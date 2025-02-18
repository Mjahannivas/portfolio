# Use the official Ubuntu base image
FROM ubuntu:latest

# Set metadata
LABEL Name=MJLemurian Version=0.0.1

# Update and install required packages
RUN apt-get -y update && \
    apt-get install -y fortunes nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Create directories
RUN mkdir -p /var/html/site

# Remove default Nginx configurations
RUN rm -rf /etc/nginx/sites-available/default && \
    rm -rf /etc/nginx/sites-enabled/default

# Set working directory
WORKDIR /var/html/site

# Copy the Nginx configuration file
COPY mj.com /etc/nginx/sites-available/mj.com

# Create symbolic link for Nginx configuration
RUN ln -sf /etc/nginx/sites-available/mj.com /etc/nginx/sites-enabled/mj.com

# Copy the static website files
COPY . /var/html/site/

# Test Nginx configuration
RUN nginx -t

# Expose port 80
EXPOSE 80

# Start Nginx in the foreground
ENTRYPOINT ["nginx", "-g", "daemon off;"]