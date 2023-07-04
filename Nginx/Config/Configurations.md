# 1️⃣Server
```
http {
        server {
            listen YOUR_PORT;
            root YOUR_ROOT;
        }
    }
```
# 2️⃣Allow Types
```
http {
		include mime.types; //!!!
        server {
            listen YOUR_PORT;
            root YOUR_ROOT;
        }
    }
```
# 3️⃣Add Locations
```
http {
        include mime.types;

        server {
            listen YOUR_PORT;
            root YOUR_ROOT;

			

			// Nginx will access root/FOLDER_NAME
			location /FOLDER_NAME { 
                
            }

			// You can also choose another root for locations
            location /FOLDER_NAME { 
                root: ANOTHER_ROOT
            }

			// You can use alias to location
            location /LOCATION_NAME {
                alias PATH_TO_LOCATION;
            }

			// You can try to get files and return status code if not found
            location /LOCATION {
                try_files FIRST_FILE SECOND_FILE =404;
            }
            
	        // Using Regex!!!
            location ~* /count/[0-9] { 
                try_files /file-you-want-to-try =404;
            }
        }
    }
```
# 4️⃣Redirect & Rewrite
```
http {
        include mime.types;

        server {
            listen YOUR_PORT;
            root YOUR_ROOT;

			// Rewrite
			rewrite ^/number/(/w+) /count/$1;

			// Nginx will access root/FOLDER_NAME
			location /FOLDER_NAME { 
                
            }

			// You can also choose another root for locations
            location /FOLDER_NAME { 
                root: ANOTHER_ROOT
            }

			// You can use alias to location
            location /LOCATION_NAME {
                alias PATH_TO_LOCATION;
            }

			// You can try to get files and return status code if not found
            location /LOCATION {
                try_files FIRST_FILE SECOND_FILE =404;
            }
            
	        // Using Regex!!!
            location ~* /count/[0-9] { 
                try_files /file-you-want-to-try =404;
            }

			// Redirect <- HERE
			location /crop {
                return 307 /fruits;
            }
        }
    }
```
# 5️⃣Load balancer

```
http {
        include mime.types;

        server {
            listen YOUR_PORT;
            root YOUR_ROOT;

			upstream backendserver {
	            server 127.0.0.1:1111;
	            server 127.0.0.1:2222;
	            server 127.0.0.1:3333;
	            server 127.0.0.1:4444;
	        }

			location / {
                proxy_pass http://backendserver/;
            }
        }
    }
```
# 6️⃣Reverse Proxy
```
http {
        include mime.types;

        server {
            listen YOUR_PORT;
            root YOUR_ROOT;


			location /LOCATION {
                proxy_pass http://192.168.x.x/anything;
            }
        }
    }
```