
---
title: Bring Traffic into a minikube cluster on a Baremetal Server
author: Zubair Ahmed
date: 2023-06-14 11:33:00 +0800
categories: [Kubernetes, DevOps]
tags: [ingress_baremetal]
math: false
mermaid: false
---

What motivated me to write, is the fact regardless of so much material on Kubernetes, I didn't find a simple example to ingress into a Kubernetes Cluster on a Bare-metal machine.

## Prerequisites 

### You should have the following to follow this example:

1. A machine with decent specs, I have used an Intel i7 HP Desktop machine with 16 GB RAM and 150 GB hard-drive.
2. having Ubuntu 22.04, with apache 2.4 installed 
3. also installed minikube version: v1.29.0
4. my machine dials to a local service provider to get a static IP assigned to it   



### Effort Required

At a highlevel we can break the efforts required into:

- [**Setup minikube**](#option-1-using-the-chirpy-starter) - Setup the minikube cluster to with appropriate Pods and Services
- [**Writing reverse proxy rules**](#option-2-forking-on-github) - Writing rules for Reverse Proxy (using Apache) to direct all the traffic to the minikube cluster. 

#### Option 1. Setting up Pods and Services

Rather than writing [**Setup minikube**] Pods and Service Configuration we will use few commands to avoid any mistakes as you follow. 

#### Option 2. Writing reverse Proxy Rules

This may already be [**Writing reverse proxy rules**]in your knowledge but we will provide what worked for us.

Lets start by starting minikube drivers:

```console
$ minikube start --driver=virtualbox
```

> If you don't want to deploy your site on GitHub Pages, append option `--no-gh` at the end of the above command.
{: .prompt-info }

Download the generated package, unzip and delete the following two from the extracted files:

- `browserconfig.xml`{: .filepath}
- `site.webmanifest`{: .filepath}

And then copy the remaining image files (`.PNG`{: .filepath} and `.ICO`{: .filepath}) to cover the original files in the directory `assets/img/favicons/`{: .filepath} of your Jekyll site. If your Jekyll site doesn't have this directory yet, just create one.

The following table will help you understand the changes to the favicon files:

| File(s)             | From Online Tool                  | From Chirpy |
|---------------------|:---------------------------------:|:-----------:|
| `*.PNG`             | ✓                                 | ✗           |
| `*.ICO`             | ✓                                 | ✗           |

>  ✓ means keep, ✗ means delete.
{: .prompt-info }

The next time you build the site, the favicon will be replaced with a customized edition.
