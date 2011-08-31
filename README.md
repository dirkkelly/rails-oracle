# Rails Oracle Sample App

## Instant Client

You will need to install the oracle instant client. Set environment variables to point to the packages

_example ORACLE_HOME, ORACLE_BASE and LD_LIBRARY_PATH locations_

    export ORACLE_HOME=/opt/oracle/instantclient
    export ORACLE_BASE=/opt/oracle/instantclient
    export LD_LIBRARY_PATH=/opt/oracle/instantclient

_download the instant client here http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html_

## TNS Names

Create a tnsnames.ora to help oracle connections identify datasources, you'll need to define the folder storing the file

_example tnsnames.ora_

    ABC =
      (DESCRIPTION =
        (ADDRESS =
          (PROTOCOL = TCP)
          (HOST = abc.tld.com)
          (PORT = 1533)
        )
      (CONNECT_DATA =
        (SID = abc)
      )
    )

_example TNS_ADMIN location_

    export TNS_ADMIN=/opt/oracle/

## Database config

    development:
      adapter: oracle_enhanced
      database: abc
      username: username
      password: password

## Model

    class Person < ActiveRecord::Base

      set_table_name  "some_owner.person_vs"
      set_primary_key "person_id"

    end

## Apache Setup

Create an apache instance

    <VirtualHost *:80>
      ServerName rails-oracle.dev
      DocumentRoot /var/www/app-name/public/
      RackEnv development
      <Directory /var/www/app-name/public/>
        AllowOverride all
        Options -MultiViews
      </Directory>
    </VirtualHost>

Add your oracle environment data to your apache config

    SetEnv ORACLE_HOME "/opt/oracle/instantclient"
    SetEnv ORACLE_BASE "/opt/oracle/instantclient"
    SetEnv LD_LIBRARY_PATH "/opt/oracle/instantclient"
    SetEnv TNS_ADMIN "/opt/oracle"