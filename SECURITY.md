# Security

Silverback Studios is young, experimental software. Treat it as a starting point, not a hardened
service.

## Reporting a vulnerability

Report it privately with GitHub's **Report a vulnerability** button (the **Security** tab of
this repository). Include the steps to reproduce it, what an attacker could do, and the commit
you tested.

Please do not post vulnerabilities in YouTube comments, public issues, discussions or social
media. The same private channel works for anything else that should not be public, such as a
file you believe infringes your rights.

## Supported versions

Only the `main` branch is supported. There are no releases or backports. Responses are best
effort: there is no bounty and no guaranteed response time.

## Deploying safely

- **Never run a public instance with the free top-up on.** Demo billing (free top-ups and
  plan upgrades) is closed by default once a gateway key is set. Do not set
  `SILVERBACK_DEMO_BILLING=on` on anything other people can reach.
- **Set a low daily budget.** `TREG_DAILY_BUDGET_USD` (default 5) caps what the server spends
  in 24 hours. Set a spending cap at the gateway as well.
- **Put an auth layer in front.** Guests and sign-ups are open, and each new account starts
  with free credits. On the internet, run Silverback Studios behind a proxy that requires sign-in (or on
  a private network), serve it over HTTPS, and set `COOKIE_SECURE=1` and `SILVERBACK_ORIGIN`.
  `deploy/start.sh` listens on `127.0.0.1` unless you set `BIND`.
- **Keep the gateway key server-side.** `TREG_TOKEN` and the other keys belong in
  `.env.local`, the server's environment, or files named by `*_FILE` settings. Never put them
  in client code, a `NEXT_PUBLIC_*` variable, a commit, a log or an issue.
- **Never point a public instance at a personal agent.** A Hermes agent's own tools (shell,
  files, memory) are not behind Silverback Studios's approval cards. Use a narrow agent on its own
  machine (see [`docs/hermes-on-orgo.md`](docs/hermes-on-orgo.md)). A live agent is closed
  until you list who may use it in `AGENT_ALLOWED_EMAILS`; keep that list short.
- **Use the narrowest Orgo key you can.** Never your main account key. Make a workspace-scoped
  key (`orgo api-keys create --workspace <id>`) for a workspace that holds only the computers
  Silverback Studios starts.
- **Never show keys on screen.** When you record, stream or take screenshots, keep
  `.env.local`, terminal output and the new-key dialog out of view. Rotate any key that was
  shown.
