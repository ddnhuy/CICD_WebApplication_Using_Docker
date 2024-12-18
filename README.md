# Configuration Steps

### Running Locally

1. **Clone the Repository**
   ```bash
   git clone https://github.com/ddnhuy/CICD_WebApplication_Docker.UI.git
   cd CICD_WebApplication_Docker.UI
   ```

2. **Install .NET Development Certificate**

   - Run the following command to install the .NET development certificate to run project locally:
   ```bash
   dotnet dev-certs https -ep $env:USERPROFILE\.aspnet\https\aspnetapp.pfx -p crypticpassword
   dotnet dev-certs https --trust
   ```

3. **Create a `.env` File**
   - Create a `.env` file in the root directory with the same variables as in `.env.example`.
   - Use the .NET development certificate: [Hosting ASP.NET Core images with Docker Compose over HTTPS](https://learn.microsoft.com/en-us/aspnet/core/security/docker-compose-https?view=aspnetcore-8.0)

4. **Install Docker and Docker Compose**
   - Make sure Docker and Docker Compose are installed on your machine. Follow the official [Docker installation guide](https://docs.docker.com/get-docker/) and [Docker Compose installation guide](https://docs.docker.com/compose/install/).

5. **Building and Running the Application using Visual Studio**
   1. **Open the Project**
      - Open the project in Visual Studio.

   2. **Build the Solution**
      - Build the solution using Visual Studio's build tools.

   3. **Run the Application**
      - Run the application using Visual Studio's run/debug tools.

6. **(Optional) Orchestrating Services using Docker Compose**
   1. **Start the Services**
      ```bash
      docker-compose up -d
      ```

   2. **Access the Application**
      - The application should be accessible at `https://your_domain:1001`.

### Setting up on VPS

Current VPS's OS: `Ubuntu 20.04`

1. **Set Up SSH**
   1. **Generate SSH Key Pair on VPS**
      ```bash
      ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
      ```
      - Follow the prompts to save the key pair in the default location (`~/.ssh/id_rsa`).

   2. **Add SSH Key to SSH Agent**
      ```bash
      eval "$(ssh-agent -s)"
      ssh-add ~/.ssh/id_rsa
      ```

2. **Obtain SSL Certificates using Let's Encrypt**
   1. **Install Certbot**
      - Follow the instructions on the [Certbot website](https://certbot.eff.org/) to install Certbot for your web server and OS.
   
   2. **Obtain SSL Certificates**
      ```bash
      sudo certbot certonly --standalone -d your_domain
      ```
      Replace `your_domain` with your actual domain name.

   3. **Locate the Certificates**
      - Certificates are typically stored in `/etc/letsencrypt/live/your_domain/`.

3. **Install Docker and Docker Compose**
   - Make sure Docker and Docker Compose are installed on your VPS. Follow the official [Docker installation guide](https://docs.docker.com/get-docker/) and [Docker Compose installation guide](https://docs.docker.com/compose/install/).

4. **Set Up GitHub Secrets**
   1. **Navigate to Your Repository on GitHub**
      - Go to the repository on GitHub.

   2. **Go to Settings**
      - In the repository, click on `Settings`.

   3. **Set Up Secrets**
      - In the `Security` section, click on `Secrets and variables`, then `Actions`.
      - Click on `New repository secret` and add the following secrets:
        - `SSH_PRIVATE_KEY`
        - `SSH_HOST`
        - `SSH_USER`

### Automatic Server Update
- After configuring everything, simply push to the `main` branch or merge your changes into the `main` branch, and the server will automatically update.

### Notes
- The pipeline will not work in the first run due to the missing `.env` file. Please set up the `.env` file similarly to the local setup.  (use the Let's Encrypt certificate) 

### Additional Steps
- **Configure Nginx**
  - Set up Nginx to point to the port where the application is running.

- **Verify Configuration**
  - Ensure that the configuration steps work as expected by running the application and its services.
- **Update README**
  - Update the README file in the repository to include these configuration steps for better guidance to contributors.
