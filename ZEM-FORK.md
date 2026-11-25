# hazem3500/doop fork notes

Branch `zem-access` = upstream `main` + two commits, kept small so it rebases:

1. `desktop/src-tauri/src/server.rs`: a build-time `DOOP_AUTH_HOSTS`
   (comma-separated) adds hosts that stay inside the app window. Needed for a
   self-host behind Cloudflare Access: upstream opens every other host in the
   system browser, so the Access cookie lands there and the app shows a
   cancelled load. Candidate for an upstream PR (not posted).
2. `.github/workflows/zem-desktop.yml`: builds the macOS arm64 Chromium shell
   with `DOOP_APP_URL=https://design.zem.cool` and
   `DOOP_AUTH_HOSTS=oz-cloud.cloudflareaccess.com`, grants IPC to
   design.zem.cool, launch-checks it on the runner and publishes a release.

The Access callback (`design.zem.cool/cdn-cgi/access/authorized`) is on the
app's own host, so it already stays in-window. Updates are off in this build
(upstream's updater only runs for doop.design builds).

Rebase: `git fetch upstream && git rebase upstream/main zem-access`.
