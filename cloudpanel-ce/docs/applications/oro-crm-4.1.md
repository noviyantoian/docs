---
id: oro-crm-4.1
title: OroCRM 4.1
sidebar_label: OroCRM 4.1
---

import useBaseUrl from '@docusaurus/useBaseUrl';

On this page, we explain step by step how to setup **[OroCRM 4.1](https://oroinc.com/orocrm/)** with **CloudPanel**.

## Installation

In the following example we will setup **[OroCRM](https://oroinc.com/orocrm/)** under the domain ***www.domain.com***.

### Preparation

Before we can start with the installation, we need to create an [SSH User](../frontend-area/users#adding-a-user), a [Database](../frontend-area/databases#adding-a-database), and a [Domain](../frontend-area/domains#adding-a-domain).

When you [Add the Domain](../frontend-area/domains#adding-a-domain), make sure to select the **OroCRM 4.1 Vhost Template** and the right **PHP Version**.

<img class="border" src={useBaseUrl('img/v1/applications/oro-crm-4.1/new_domain.png')} /> <br /><br />

:::warning Document Root
Make sure to point the **Document Root** to the **public** directory.
:::

### Installation

To install **OroCRM** do the following steps:

1. [Login via SSH](../frontend-area/users#ssh-login) to the server e.g. with **john-ssh** and go to the **htdocs** directory:

```
cd /home/cloudpanel/htdocs/
```

2. Delete the project directory which has been created by **CloudPanel**:

```
rm -rf /home/cloudpanel/htdocs/www.domain.com
```

3. Clone latest **4.1.x** version from **github**:

```
git clone -b 4.1.10 https://github.com/oroinc/crm-application.git www.domain.com
```

:::caution Latest Version
You find the latest version on github: [https://github.com/oroinc/crm-application/releases](https://github.com/oroinc/crm-application/releases)
:::

4. Install via **composer**:

```
cd /home/cloudpanel/htdocs/www.domain.com/
php7.4 /usr/local/bin/composer install --prefer-dist --no-dev
```

4. Enter the **database credentials** and other **parameters**:

<img class="border" src={useBaseUrl('img/v1/applications/oro-crm-4.1/application_parameters.png')} /> <br /><br />

5. Run **oro:install** command:

```
php7.4 /home/cloudpanel/htdocs/www.domain.com/bin/console oro:install --env=prod --timeout=8000
```

Enter the **Application URL**, **Organization name** and the admin **Username** and **Password**:

<img class="border" src={useBaseUrl('img/v1/applications/oro-crm-4.1/enter_application_data.png')} />

6. Reset permissions.

```
cd /home/cloudpanel/htdocs/
clpctl system:permissions:reset www.domain.com 775
```

7. Done! You can now open your domain in your browser and start working with **OroCRM**.

<img class="border" src={useBaseUrl('img/v1/applications/oro-crm-4.1/admin_login.png')} />