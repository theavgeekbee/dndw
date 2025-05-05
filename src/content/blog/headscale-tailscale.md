---
title: 'dndw: headscale + tailscale'
description: '"For the wrath of God is revealed from heaven against all ungodliness and unrighteousness of men, who by their unrighteousness suppress the truth." - Romans 1:18'
ord: 0
---
# dndw: headscale + tailscale
> "Freedom is the freedom to say that <r>two plus two</r> make <bl>four</bl>. If that is granted, <y>all else follows</y>."
> 
> &mdash; George Orwell, 1984

<r>Tailscale</r> is a great tool for cybersecurity nerds like me. I especially use it to <bl>securely link</bl> all of my devices
on my own home network. This is great especially for when I'm <r>trading</r>, and I want to be sure that my financial data
is <bl>extremely secure</bl>.

## that's great! is there any way to self-host a server?
That's a great question!

I actually do <bl>self-host</bl> my own tailscale server for when I'm <r>away from home</r>.
<r>Headscale</r> makes it <bl>really easy</bl> to set up my own server and connect to it.

## what do I need to get started?
You're going to want <r>two things</r> for this:
- A VPS or server (I use [DigitalOcean &#8599;](https://digitalocean.com/))
- A domain

## i have those things. how do I get started?
1. Allocate a new VPS and assign a <r>static IP</r>. Link this IP to your desired subdomain using an <r>A</r> record (if you're using Cloudflare, deselect <bl>proxy</bl>).
2. [Install Headscale &#8599;](https://headscale.net/stable/)
3. Make the following changes to the config file:
    - Set `server_url: https://your.domain.io:443`
    - Set `listen_addr: 0.0.0.0:443`
    - In derp, enable <r>server</r> and set <r>ipv4</r> to your <bl>assigned static IP</bl>
    - Set the acme_email and `tls_letseencrypt_hostname: your.domain.io`
4. Restart Headscale using `sudo systemctl restart headscale`
5. Install <bl>Tailscale</bl> on the server
6. Register the server as an exit node using `sudo tailscale up --login-server https://your.domain.io --advertise-exit-node`
7. <bl>Log the server in</bl> using a <r>separate shell</r>
8. Run `sudo tailscale set --advertise-exit-node` and then `sudo tailscale down`
9. List the routes using `headscale routes list`
10. For <r>every named node</r>, run `headscale routes enable -r <id>` for its ID.
11. Start Tailscale using the <bl>previous tailscale command</bl>

## how do I connect?
On your <r>own computer</r>, run `sudo tailscale up --login-server https://your.domain.io --exit-node <node-name>`.
Log the client in.
The <r>node name</r> is the one that's named in the previous <bl>step 9</bl>.

## privacy ~ freedom
To add a footnote, I'd like to assert that <r>privacy</r> and <bl>freedom</bl> go hand in hand.
When <bl>freedom</bl> is given, you must fight for your right to <r>privacy</r>. 

Tailscale gives you <bl>freedom</bl>; use it to gain your <r>privacy</r>.
