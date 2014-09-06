Steps to install Bahmni (OpenMRS and OpenELIS): (SHR omods won't be installed)

> git clone --recursive https://github.com/SharedHealth/Bahmni-Server.git
> cd Bahmni_Server
> cd bdshr_config && ./scripts/package.sh
> cd .. && vagrant up --no-provision

Bahmni recommends disk space of min 30GB (https://gist.github.com/christopher-hopper/9755310)

On guest machine /packages should contain localrepo, servers, tools and python-packages. Make sure /packages has the required permissions. Copy the dirs from blrfs01/teamshares/bahmni.

On host machine /var/lib/bahmni/release/bahmni-{{release_version}}.zip should be present. Copy the zip from blrfs01/teamshares/bahmni or bangladesh. Make sure the file has the required permissions.

> vagrant provision

Manual steps - https://sharedhealth.atlassian.net/wiki/display/docs/Manual+steps+after+new+bahmni+installation
