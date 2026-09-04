# Moek IPTV — updates

Hier haalt de app zijn eigen updates vandaan. Elke editie is een aparte app met
een eigen versienummer, dus elke editie heeft zijn eigen map:

    moek/version.json     moek/app.apk
    moena/version.json    moena/app.apk
    shreya/version.json   shreya/app.apk

De app leest `version.json`, vergelijkt `versionCode` met wat er geïnstalleerd
staat, en biedt de nieuwe versie aan als die hoger is. Android vraagt daarna
altijd zelf om bevestiging voordat er iets geïnstalleerd wordt.

## Waarom dit openbaar mag

Deze bestanden bevatten geen abonnement en geen inloggegevens. Die zaten
vroeger in de app om de eerste installatie makkelijk te maken; ze staan nu
alleen nog in de database op het toestel zelf, en die blijft staan bij een
update.

Een build **mét** abonnement wordt bewust gemaakt en hoort hier **niet**:

    ./gradlew :app:assembleShreyaRelease -PbundleSubscription=true

Zo'n bestand gaat met de hand naar het toestel in kwestie. De versleuteling
erin is een drempel, geen slot.

## Nieuwe versie plaatsen

1. `./gradlew :app:assembleMoekRelease :app:assembleMoenaRelease :app:assembleShreyaRelease`
2. De APK's hierheen kopiëren als `<editie>/app.apk`
3. `versionCode` en `versionName` in `<editie>/version.json` bijwerken
4. Committen en pushen naar `main`
