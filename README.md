# The rtcamp script is designed to setup a wordpress webserver with little interaction or configuration from the end user
# The following components are used to setup the webserver:
# 1) mysql
# 2) Nginx
# 3) php
# 4) wordpress
# The webserver that will be configured is fairly basic - it does not use a proxy, or reverse proxies.  It will not configure SSL
# It will add an entry into your host file for the domain name of choice on the loopback address (127.0.0.1) so that the user can
# Launch the website locally.
# A few assumptions were used in the creation of the script
# 1) That PHP 7.2 would be used
# 2) That basic Nginx would be used
# 3) The website would not be secured in an appropriate manner to be published on the web with sensitive data
# 4) That the user can read and follow the prompts reasonably well, and follow the instructions on screen in english
# 5) The script does not require that the mysql_secure_installtion utility be run.  It does prompt the user if they should
# like to enter and configure - they may, however it is not required.  Therefore there are obvious security holes as a result 
# of not taking this path.  As mentioned above -its not secured for public presentation
# 6) The Nginx sites-avilable/enabled configuration is quite basic.  If more exotic or robust implementations are necessary
# script can be modified for that
# 7) This server is not part of a distributed webserver setup, or clustered setup to handle high volume traffic.  This creates
# a standalone server.
# 8) The user is capable of entering a proper domain name when prompted.  The script does not validate .com,.org,.ca,.biz etc - as # there are too many permutations to cover.  Therefore when the script prompts for a domain name it is assumed the user will know # what to enter
# 9) Strong password encryption parameters were incorporated into the script.  This means that the user password generated for the # DB is a Strong password.  The script does not allow for the user to enter their own password.  If that is desired, the script can # easily be modified
# 10) There was a challenge in getting the sed command to update the wp-config file - likely due to the Strong password.The script # was modified in order to successfully insert the password in the wp-config file, however its possible that under certain password # permutations it may revert to behaviour where the 'password_here' in the default file gets inserted into the middle of the Strong # password.  If the user runs the script and gets an error attempting to establishing the database connection - this is likely the # cause, and the wp-config.php file simply needs to be edited
#11) The script can be run from the /home/$user/ directory. Chmod +x has been applied, the author assumes that will hold, but
# it was not tested.  You may also need to assign appropriate permissions to the file to execute it
#12) The wordpress files will be inserted into /var/www/${domain}  where ${domain} is the domain name that the user enters during    # the script execution
