# deploy-railway-flyio

FLY.IO:

	https://fly.io/docs/hands-on/install-flyctl/
	
	1) Install:
	
			curl -L https://fly.io/install.sh | sh

		1.1) configured: home/youruser/.Bashrc:
		
			export FLYCTL_INSTALL="/home/youruser/.fly"
			export PATH="$FLYCTL_INSTALL/bin:$PATH"

		1.2) Terminal:
		
			source ~/.bashrc
			
		1.3) register on web (with github)
		
			https://fly.io/
			add a debit or credit card
			
		1.4) login on terminal vscode:
		
			flyctl auth login
		
	
	2) Deploy
		
		fly launch
		
			config name of project
			choose a region
			choose a plan
			create db postgresql
			
		fly deploy
		
		
	3) Config volumes
	
		fly volumes create eshop_whth_flyio
		
		3.1) paste on file fly.toml, (((https://fly.io/docs/reference/volumes/)))
		
			[mounts]
			source="myapp_data"
			destination="/data"
			Railway:
			
		3.1.2) in file.toml replace "myapp_data" with your name of volumes
		3.1.3) in file config/storage.yml replace "storage" whith "/data"
		3.1.4) fly deploy

RAILWAY
	1) Create account (with github)
		
		https://railway.app/
		add a debit or credit card
		
	2) Deploy
		
		2.1) in your project create file:
			Procfile
				web: rake db:migrate && bin/rails server -b 0.0.0.0 -p ${PORT:-3000}
				
		2.2) database.yml
		
			production:
			  <<: *default
			  url: <%= ENV["DATABASE_URL"] %>
			  database: railwayapp_production
			  username: railwayapp
			  password: <%= ENV["RAILWAYAPP_DATABASE_PASSWORD"] %>
			  
		2.3) create repo in github and push project
		2.4) solved first error, create a file railway.json with:
		
			{
			    "$schema": "https://railway.app/railway.schema.json",
			    "build": {
			      "builder": "NIXPACKS"
			    },
			    "deploy": {
			      "restartPolicyType": "ON_FAILURE",
			      "restartPolicyMaxRetries": 10
			    }
			}
		2.5) git add, commit and push
		2.6) solved second error, add in development.rb and production.rb:
		
			config.hosts << "eshop-production-7696.up.railway.app"
		2.7) git add, commit and push
