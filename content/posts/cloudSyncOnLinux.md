---
title: Cloud Sync On Linux
date: 2019-01-07
published: true
tags: ['cloud', 'linux', 'sync']
series: false
# cover_image: ./images/alexandr-podvalny-220262-unsplash.jpg
canonical_url: false
description: "Living on the cloud seems like an idea, let's give it a try."
---

<!-- # Cloud Sync On Linux -->

There was a time when living with portable Hard Drives was considered hip. That time has passed, we for one live on clouds; therefore our data should also be located nearby, on a cloud or something.

I've been wanting to setup cloud based backup on my machines for quite some time now. This offers numerous benefits, e.g

* Minimum time is wasted in configuring new machines
* You can save your settings for all future machines in advance
* You could even use this stuff in docker and subsequently on the web

Most linux machines come with a tool called [rsync](https://wikipedia.org/wiki/Rsync) which can be used to sync files from one location to another. However the utility is not designed to work with cloud storage, therefore after a little internet hunting I found [Rclone](https://rclone.org/) -  a command line utility designed specifically to sync to cloud.

Now let's setup [Rclone](https://rclone.org/) and backup our folders to the cloud.

## Process

### Installation

Head over to [https://rclone.org/install](https://rclone.org/install) to get install instructions. You will have to do this step depending on your OS / distro. On linux it is just a script install command, which is super easy to do.
```bash
curl https://rclone.org/install.sh | sudo bash
```

>This is why I love linux, even the damn install script is hosted *online*. I almost miss downloading useless installers and big assed packages.

Now verify the installation by typing `rclone` in any terminal.