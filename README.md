# Gitlab and AWX Demo

I recently had cause to expain how an AWX and GitOps environment might work. To help with that, I built this demo environment.

The Vagrantfile works, but is quite memory constrained.

The Ansible Playbook creates the following environment:

* Services
  * Gitlab - HTTP only, on http://<yourip>:1080
  * AWX - HTTP only, on http://<yourip>
* Users (Password: `Sup3rSecr3t`)
  * (Gitlab only) root - Admin account
  * (Gitlab only) awx - Service account for AWX connection
  * csa, ops, release - User accounts for AWX and Gitlab
  * (AWX only) admin - Admin account

It does not "connect" AWX to Gitlab, aside from creating an AWX credential.

## Todo

Please see the issues page for a list of enhancements that would be good to implement!
