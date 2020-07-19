# oereb2-dev
Temporary stuff

## Start Datenbank
```
docker run --rm --name oereb-db -p 54321:5432 --hostname primary \
-e PG_DATABASE=oereb -e PG_LOCALE=de_CH.UTF-8 -e PG_PRIMARY_PORT=5432 -e PG_MODE=primary \
-e PG_USER=admin -e PG_PASSWORD=admin \
-e PG_PRIMARY_USER=repl -e PG_PRIMARY_PASSWORD=repl \
-e PG_ROOT_PASSWORD=secret \
-e PG_WRITE_USER=gretl -e PG_WRITE_PASSWORD=gretl \
-e PG_READ_USER=ogc_server -e PG_READ_PASSWORD=ogc_server \
-v /tmp:/pgdata:delegated \
sogis/oereb2-db:latest
```

## Zuständige Stellen
Schema anlegen:
```
 java -jar /opt/ili2pg-4.3.1/ili2pg-4.3.1.jar --dbhost localhost --dbdatabase oereb --dbport 54321 --dbusr admin --dbpwd admin --nameByTopic --defaultSrsCode 2056 --modeldir "../oereb2-db/models/;http://models.geo.admin.ch" --models OeREBKRM_V2_0 --dbschema oereb_zustaendige_stellen --schemaimport
```

Daten manuell erfassen für Wisen (2502) und Messen (2457), das ARP, das AGI und die Staatskanzlei.

Export:
```
java -jar /opt/ili2pg-4.3.1/ili2pg-4.3.1.jar --dbhost localhost --dbdatabase oereb --dbport 54321 --dbusr admin --dbpwd admin --modeldir "../oereb2-db/models/;http://models.geo.admin.ch" --models OeREBKRM_V2_0 --dbschema oereb_zustaendige_stellen --export ch.so.agi.zustaendigestellen.oereb2.xtf

xmllint --format ch.so.agi.zustaendigestellen.oereb2.xtf -o ch.so.agi.zustaendigestellen.oereb2.xtf
```

## Konfiguration ("Annex-Modell"): Gemeinden mit ÖREB
Schema anlegen:
```
 java -jar /opt/ili2pg-4.3.1/ili2pg-4.3.1.jar --dbhost localhost --dbdatabase edit --dbport 54321 --dbusr admin --dbpwd admin --nameByTopic --defaultSrsCode 2056 --modeldir "../oereb2-db/models/;http://models.geo.admin.ch" --models OeREBKRMkvs_V2_0 --dbschema oereb_konfiguration --schemaimport
```

Daten manuell erfassen.

Export:
```
java -jar /opt/ili2pg-4.3.1/ili2pg-4.3.1.jar --dbhost localhost --dbdatabase edit --dbport 54321 --dbusr admin --dbpwd admin --modeldir "../oereb2-db/models/;http://models.geo.admin.ch" --models OeREBKRMkvs_V2_0 --dbschema oereb_konfiguration --export ch.so.agi.gemeinden.oereb2.xtf

xmllint --format ch.so.agi.gemeinden.oereb2.xtf -o ch.so.agi.gemeinden.oereb2.xtf
```

```
java -jar /Users/stefan/apps/ilivalidator-1.11.6/ilivalidator-1.11.6.jar --modeldir "http://models.geo.admin.ch;https://raw.githubusercontent.com/oereb/oereb2-ilirepo/master/" ch.so.agi.gemeinden.oereb2.xtf
```

## Konfiguration ("Annex-Modell"): Logos und MapLayering
Schema anlegen:
```
java -jar /opt/ili2pg-4.3.1/ili2pg-4.3.1.jar --dbhost localhost --dbdatabase edit --dbport 54321 --dbusr admin --dbpwd admin --nameByTopic --defaultSrsCode 2056 --modeldir "../oereb2-db/models/;http://models.geo.admin.ch" --models OeREBKRMkvs_V2_0 --dbschema oereb_konfiguration_logo --schemaimport
```

Daten manuell erfassen.

Export:
```
java -jar /opt/ili2pg-4.3.1/ili2pg-4.3.1.jar --dbhost localhost --dbdatabase edit --dbport 54321 --dbusr admin --dbpwd admin --modeldir "../oereb2-db/models/;http://models.geo.admin.ch" --models OeREBKRMkvs_V2_0 --dbschema oereb_konfiguration_logo --export ch.so.agi.konfiguration.oereb2.xtf

xmllint --format ch.so.agi.konfiguration.oereb2.xtf -o ch.so.agi.konfiguration.oereb2.xtf
```

```
java -jar /Users/stefan/apps/ilivalidator-1.11.6/ilivalidator-1.11.6.jar --modeldir "http://models.geo.admin.ch;https://raw.githubusercontent.com/oereb/oereb2-ilirepo/master/" ch.so.agi.konfiguration.oereb2.xtf
```
