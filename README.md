# Task :3 Encryption  command
## Task3 Document


Set Up Decryption Environment
Step 1: Install Required Packages
Update your package list:


```bash

sudo apt update
```

# Install Apache

```bash
sudo apt install apache2
```

```bash
sudo apt install php libapache2-mod-php
Install OpenSSL (if not already installed):
```

```bash
sudo apt install openssl
```
# Step 2 Download Required Files
Download the following files from your Drive folder to your local machine:
decrypt.php
index.html
symmetric_key.txt
message.enc
# Step 3: Create the Encrypted Directory
Run the command to create a directory named encrypted:

```bash
sudo mkdir -p /var/www/html/encrypted
```
Move to the Downloads Directory
Navigate to the directory where you downloaded the files.


# Step 5: Copy the Encrypted Message File
Copy message.enc to the /var/www/html/encrypted directory:

```bash
Copy code
sudo cp message.enc /var/www/html/encrypted/message.enc
```
# Step 6: Rename Existing index.html
Rename the existing index.html file in /var/www/html:

bash
sudo mv /var/www/html/index.html /var/www/html/index_old.html
# Step 7: Copy the decrypt.php File
Copy decrypt.php from the Downloads directory to /var/www/html/:

bash
sudo cp decrypt.php /var/www/html/decrypt.php
Ensure you are in the Downloads directory while executing this command.

# Step 8: Copy the New index.html
Now, copy the new index.html file into the /var/www/html directory:

bash
sudo cp index.html /var/www/html/index.html
Ensure you are currently in the Downloads directory.

# Step 9: Configure Apache for Custom Header
Open the Apache configuration file:



sudo vim /etc/apache2/sites-available/000-default.conf
Add the following content inside the <VirtualHost> block:

apache

<Directory "/var/www/html">
    Header always set X-Symmetric-Key "Your-Symmetric-Key-Header"
</Directory>
Your file should look like this:

apache

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    <Directory "/var/www/html">
        Header always set X-Symmetric-Key "Your-Symmetric-Key-Header"
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
# Step 10: Enable Apache Modules and Restart
Run the following commands one by one:

bash

sudo a2enmod rewrite
sudo systemctl restart apache2
# Step 11: Testing the Setup
Open your web browser and navigate to:

http://localhost/index.html
Select the symmetric_key.txt file containing your symmetric key from the Downloads directory.

Click the "Decrypt" button to see the decrypted content displayed on the page.

# Step 12: Testing with Curl
To test the decryption using curl, run the following command in your terminal:

```bash

curl -X GET \
-H "X-SYMMETRIC-KEY: $(cat symmetric_key.txt)" \
http://localhost/decrypt.php
Ensure you are in the Downloads directory when executing this command, as it requires the correct path to symmetric_key.txt.
```
