## Changes Implemented to better suit asahi
- double hashing prevention 
    - sometimes passwords were being double hashed when an auth object was being updated twice 
        - before update was being called twice, therefore hashing the hashed password 
        - this is fixed with a bcrypt REGEX tester that was a solution others used. 
            - small use case of someone with a bcrypt hashed pw already isn't going to get hashed
- changed login.js to prevent blocked users from logging in 
    - can be taken care of in policies, but this is root level prevention which is safer/ more reliable in case a policy is forgotten on a route
- compatibility with facebook auth
    - facebook auth model does not require a password, so when a user tries to login with an empty password and their facebook email, they could get in
    - now there is a check on login.js for empty passwords, which also relates to the waterline error that doesn't test validations on empty or null attributes (even min length!)
- register.js 
    - prevent empty password at time of registration 
        - can be checked front end but really? why would any auth system allow an empty password to sneak through.... 
        - this was allowed becuase of the waterline logic referenced above 
- reset password token is one time use 
    - removes reset token from user and sends the token in the url 
    - prevents the user from using the same link again to reset their password 
    
