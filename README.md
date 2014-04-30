# Wildfly Cookbook
Cookbook to deploy Wildfly Java Application Server

# Requirements
Chef Client 11+

Java Opscode Community Cookbook

# Platform
- CentOS, Red Hat, Fedora
- EC2 Amazon Linux AMI

Tested on:
- CentOS 6.5

# Usage
You can add users in the proper format to `attributes\users.rb`

You can customize the Java version, and the Connector/J if you'd like.

# Attributes
* `node['wildfly']['base']` - Base directory to run Wildfly from

* `node['wildfly']['version']` - Specify the version of Wildfly
* `node['wildfly']['url']` - URL to Wildfly tarball
* `node['wildfly']['checksum']` - SHA256 hash of said tarball

* `node['wildfly']['user']` - User to run Wildfly as.
* `node['wildfly']['group']` - Group which owns Wildfly directories
* `node['wildfly']['server']` - Name of service and init.d script for daemonizing

* `node['wildfly']['mysql']['enabled']` - Boolean indicating Connector/J support

* `node['wildfly']['int'][*]` - Various hashes for setting interface & port bindings

* `node['wildfly']['smtp']['host']` - SMTP Destination host
* `node['wildfly']['smtp']['port']` - SMTP Destination port


# Recipes
* `::default` - Installs Java & Wildfly.  Also installs Connector/J if you've got it enabled.
* `::install` - Installs Wildfly.
* `::mysql_connector` - Installs Connector/J into appropriate Wildfly directory.

# Providers

Datasource LWRP

```ruby
wildfly_datasource 'example' do
  jndiname "java:jboss/datasource/example"
  drivername "some-jdbc-driver"
  connectionurl "jdbc:some://127.0.0.1/example"
end
```

Deploy LWRP

Allows you to deploy JARs and WARs via chef

Example 1 (from a url)
```ruby
wildfly_deploy 'jboss.jdbc-driver.sqljdbc4_jar' do
      url "http://artifacts.company.com/artifacts/mssql-java-driver/sqljdbc4.jar"
end
```

Example 2 (from disk)
```ruby
wildfly_deploy 'jboss.jdbc-driver.sqljdbc4_jar' do
      path "/opt/resources/sqljdb4.jar"
end
```

# Author

Author:: Brian Dwyer - Intelligent Digital Services
