Student Number : 661519
Configuration Details
Accounts Created:
marketing: Configured with an SSH key for secure file uploads to the web server's directory.
design: Configured with an SSH key and restricted shell access, limiting them to their home directory.
audit: Configured with an SSH key and set up for SFTP-only access to specific directories.

Account Removal:
sysadmin: The account was deleted, along with its associated home directory.

Permissions Overview:
marketing: Granted write permissions to /srv/www (web server directory). No access to design or audit directories.
design: Full read/write access to their own home directory, but restricted from accessing the web server directory.
audit: Read-only access to the home directories of marketing and design, as well as /srv/www.

Secure File Transfers:
SFTP is configured with a restricted shell (/usr/lib/openssh/sftp-server) for secure file handling.

Web Server Configuration
Nginx Setup:
Installed and configured Nginx to serve static content.
Document root: /srv/www.
A directory /srv/www/student/ was created with a static file containing 661519.
Verified access via the following URLs:
http://[VM_IP]/student/
http://student-661519-vm1.net.dcs.hull.ac.uk/student/

Nginx Customizations:
Added a basic server block for the root domain (student-661519-vm1.net.dcs.hull.ac.uk).
Set up Nginx as a reverse proxy:
Root domain serves static content.
Subdomain (docker.student-661519-vm1.net.dcs.hull.ac.uk) forwards requests to a Docker application on port 3000.

Docker Deployment
Installed Docker and cloned the repository from https://github.com/sbrl/SDI-Docker.git.
Built and deployed the Docker container.
Configured Docker to launch automatically during system boot.

Maintenance Instructions
Managing Users:
Update a user password: sudo passwd [username].
Add a new user: sudo useradd [username].
Delete a user and their files: sudo userdel -r [username].

Nginx Management:
Restart the server: sudo systemctl restart nginx.
Update web server content: Place files in /srv/www/.
Monitor logs: sudo tail -f /var/log/nginx/access.log.

Docker Administration:
Check active containers: docker ps.
Restart a container: docker restart [container_id].
Pull updates: docker pull [repository/image].

SFTP Monitoring:
Monitor SFTP activity: journalctl -u sshd.
Modify permissions as needed using chmod and chown.
Notes

SSH keys for each user are stored in ~/.ssh/authorized_keys.
The /srv/www directory is owned by the www-data group, with write access limited to the marketing account.
Docker configurations are stored in /etc/docker/ for easy management.
Firewall settings (ufw) did not allow traffic only on ports 22 and 80 for enhanced security.
