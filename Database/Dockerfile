FROM  postgres:13

ENV POSTGRES_USER = admin
ENV POSTGRES_PASSWORD=123456
ENV POSTGRES_DB=mydatabase

COPY init.sql /docker-entrypoint-initdb.d/ 

                          # Description

# Line 1
# FROM postgres:13
# What does it do?

# This tells Docker to use the official PostgreSQL version 13 image as the base image.

# Think of it as downloading a ready-to-use PostgreSQL server.

# Docker Hub
#      │
#      ▼
# postgres:13
#      │
#      ▼
# Linux OS
# +
# PostgreSQL Installed

# When you run the container, PostgreSQL is already installed and ready to start.

# Why PostgreSQL?

# PostgreSQL is:

# Open source
# Highly reliable
# ACID compliant
# Widely used in production
# Supports large-scale applications

# Companies like Apple, Instagram, Spotify, and Reddit use PostgreSQL for many workloads.

# Line 2
# ENV POSTGRES_USER=admin
# Purpose

# Creates the PostgreSQL administrator username.

# Username = admin

# Whenever the backend connects, it uses:

# admin

# instead of the default postgres user.

# Line 3
# ENV POSTGRES_PASSWORD=123456

# Sets the database password.

# Username : admin
# Password : 123456

# Your backend uses the same password when connecting.

# Line 4
# ENV POSTGRES_DB=mydatabase

# Creates a database automatically when the container starts for the first time.

# Without this:

# postgres

# With this:

# mydatabase

# So after the first startup, you'll have:

# PostgreSQL
# │
# ├── postgres
# └── mydatabase
# Line 5
# COPY init.sql /docker-entrypoint-initdb.d/

# This is one of PostgreSQL Docker's most useful features.

# It copies:

# init.sql

# into:

# /docker-entrypoint-initdb.d/

# When the PostgreSQL container starts for the first time (with an empty data directory), it automatically executes every .sql file found in that directory.

# Example

# Suppose your init.sql contains:

# CREATE TABLE students(
#     student_id SERIAL PRIMARY KEY,
#     first_name VARCHAR(50)
# );

# INSERT INTO students(first_name)
# VALUES('Rahul');

# When the container starts:

# Container Start
#         │
#         ▼
# PostgreSQL Starts
#         │
#         ▼
# Checks /docker-entrypoint-initdb.d/
#         │
#         ▼
# Finds init.sql
#         │
#         ▼
# Runs SQL
#         │
#         ▼
# Creates Tables
#         │
#         ▼
# Inserts Initial Data

# No manual SQL execution is needed.

# Folder Structure

# Your project likely looks like:

# database/
# │
# ├── Dockerfile
# └── init.sql

# During the build:

# database/
# │
# ├── Dockerfile
# └── init.sql
#        │
#        ▼
# Docker Image
#        │
#        ▼
# Container
#        │
#        ▼
# /docker-entrypoint-initdb.d/init.sql
# Connection with Backend

# Your backend uses:

# postgresql://admin:123456@my_postgres:5432/mydatabase

# Breaking it down:

# Value	Comes From
# admin	POSTGRES_USER
# 123456	POSTGRES_PASSWORD
# mydatabase	POSTGRES_DB
# my_postgres	Docker Compose service name
# 5432	PostgreSQL default port

# Everything matches correctly.

# Real-Time Company Flow
# Frontend
#      │
#      ▼
# Flask Backend
#      │
#      ▼
# PostgreSQL Container
#      │
#      ▼
# Database Files

# During deployment:

# docker-compose up
#       │
#       ▼
# Database Container Starts
#       │
#       ▼
# Creates Database
#       │
#       ▼
# Runs init.sql
#       │
#       ▼
# Backend Starts
#       │
#       ▼
# Backend Connects Successfully
# What Happens the First Time?
# docker-compose up
#         │
#         ▼
# Create PostgreSQL Container
#         │
#         ▼
# Create User
#         │
#         ▼
# Create Database
#         │
#         ▼
# Run init.sql
#         │
#         ▼
# Ready for Backend
# What Happens on Restart?

# If you're using a Docker volume for PostgreSQL data:

# docker stop
# docker start

# PostgreSQL does not run init.sql again because the database already exists. The initialization scripts in /docker-entrypoint-initdb.d/ are only executed when the data directory is empty.

# Production Best Practices

# Instead of hardcoding credentials:

# ENV POSTGRES_USER=admin
# ENV POSTGRES_PASSWORD=123456

# companies usually use:

# Docker Compose environment variables
# .env files
# Secret managers (AWS Secrets Manager, Kubernetes Secrets, HashiCorp Vault)

# This avoids storing passwords directly in the image.
# 

