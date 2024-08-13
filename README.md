# quicksart-customer-reviews
Run this script to set up this demo in your trial account

```sql
CREATE API INTEGRATION IF NOT EXISTS HOL_GITHUB_INTEGRATION
    API_ALLOWED_PREFIXES = ('https://github.com/sfc-gh-jgriffith')
    API_PROVIDER = git_https_api
    ENABLED = TRUE
    ;

grant usage on integration HOL_GITHUB_INTEGRATION to role ACCOUNTADMIN;

create database if not exists git ;

CREATE OR REPLACE GIT REPOSITORY git.public.ml_functions
  ORIGIN = 'https://github.com/sfc-gh-jgriffith/quickstart-ml-functions.git'
  API_INTEGRATION = HOL_GITHUB_INTEGRATION;

execute immediate from @git.public.ml_functions/branches/main/setup.sql;
```
