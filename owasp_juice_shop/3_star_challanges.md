1. Login as bender@juice-sh.op (**3 star**)

- Same as 1.
- Instead of writing `'OR 1+1--` we can simply write `bender@juice-sh.op'--`.
- This statement will return to true always when the email is a valid one.

2. Admin Registration (**3 star**)

- Register a user with admin privileges.
- Go to the register page.
- Fill all the field and submit the form.
- Intercept the request using burpsuite.
- Add a new field `role` with value `admin` in the request.
- Forward the request.
- You will be registered as admin.
- Challenge completed.
