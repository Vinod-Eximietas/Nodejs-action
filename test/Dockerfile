# Use an official Node.js runtime as the base image
FROM node:14-slim

# Set the working directory in the container
WORKDIR /app

# Create a user and group with unique UID and GID
RUN groupadd -g 15002 grpid_group && \
    useradd -u 150002 -g grpid_group usrid_user

# Copy the Node.js script into the container
COPY hello.js /app/hello.js

# Install ESLint
RUN npm install --no-cache-dir -g eslint

# Install project dependencies
COPY package.json package-lock.json /app/
RUN npm install

# Restrict app src permissions to in-container user
RUN chown -R usrid_user:grpid_group /app
RUN chmod 755 /app

# Set container user uid/gid
USER usrid_user:grpid_group

# Run ESLint to lint the Node.js script
CMD ["eslint", "--fix", "--ext", ".js", "/app"]
