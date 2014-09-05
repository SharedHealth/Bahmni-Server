01. > git clone --recursive https://github.com/SharedHealth/Bahmni-Server.git
02. > cd Bahmni_Server
03. > cd bdshr_config && ./scripts/package.sh
04. > cd ../openmrs-module-bdshrclient && mvn clean package
05. > cd ../openmrs-module-terminology_atomfeed_client && mvn clean package
06. > cd .. && vagrant up --no-provision
    Bahmni recommends disk space of min 30GB (https://gist.github.com/christopher-hopper/9755310)
07. On guest machine /packages should contain localrepo, servers, tools and python-packages.
    Make sure /packages has the right privileges. (sudo chown vagrant:vagrant /packages)
    Copy the dirs from blrfs01/teamshares/bahmni
08. On host machine /var/lib/bahmni/release/bahmni-{{release_version}}.zip should be present
    Copy the zip from blrfs01/teamshares/bahmni or bangladesh
09. > vagrant provision
