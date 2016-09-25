# Secure Development

We need a way to have a secure and non-repudiatable mechanism of writing code and pushing it into production.

The main characteristic should be that the development environments are completely isolated from the production environments.

- Remote Access to code, including commits
- Audit and reliable identity proof of commits
- Allow multiple authors on a commit (for pairing)
- Allow for tamper-proof verification of code (e.g. by a security review or automated process)

## Git

### Multiple Authors

https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=451880

### Signing Commits

### Signed Off By

### Pull requests?

Could potentially use pull requests for very secure and controlled code. I.e. have a much smaller number of authorised devs.

## Separating sensitive code?

How sensitive is code really?

Often see desire to maintain a separate repo for internal highly secure code. This adds to a barrier between the devs and the code.

What circumstances would this really be appropriate for?

- Proprietry high value algorithms - e.g. provide business unique competetive advantage
- Security algorithms (e.g. token generatation)

- Business logic? Seems unlikely

If have to do it, wrap in a api  and provide fakes for general dev. INcreased complexity in integration pipeline.


