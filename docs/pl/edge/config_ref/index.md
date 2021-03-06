* * *

license: Licensed to the Apache Software Foundation (ASF) under one or more contributor license agreements. See the NOTICE file distributed with this work for additional information regarding copyright ownership. The ASF licenses this file to you under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

           http://www.apache.org/licenses/LICENSE-2.0
    
         Unless required by applicable law or agreed to in writing,
         software distributed under the License is distributed on an
         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
         KIND, either express or implied.  See the License for the
         specific language governing permissions and limitations
    

## under the License.

# Plik config.xml

Wiele aspektów zachowania aplikacji mogą być sterowane z pliku konfiguracji globalnej `config.xml` . Ten plik XML platformy agnostyk jest ułożone, oparty na specyfikacji W3C [Pakowane aplikacji sieci Web (wzory)][1] i rozszerzone, aby określić podstawowe funkcje Cordova API, wtyczki i ustawienia specyficzne dla platformy.

 [1]: http://www.w3.org/TR/widgets/

Projekty utworzone za pomocą CLI Cordova (opisane w interfejs wiersza poleceń) ten plik można znaleźć w katalogu najwyższego poziomu:

        app/config.xml
    

Należy pamiętać, że przed wersja 3.3.1-0.2.0, plik istniał w `app/www/config.xml` , i że o to tutaj jest nadal obsługiwane.

Podczas tworzenia projektu za pomocą CLI, wersje tego pliku biernie są kopiowane do różnych `platforms/` podkatalogi, na przykład:

        app/platforms/ios/AppName/config.xml
        app/platforms/blackberry10/www/config.xml
        app/platforms/android/res/xml/config.xml
    

Ta sekcja zawiera opcje konfiguracji globalnej i przekreślać platforma szczegóły. Zobacz następujące sekcje dla poszczególnych platform opcje:

*   Konfiguracja iOS
*   Konfiguracja dla platformy Android
*   Konfiguracja blackBerry 10

Oprócz różnych konfiguracji opcji poniżej można również skonfigurować zestaw podstawowych aplikacji obrazów dla każdej platformy docelowej. Aby uzyskać więcej informacji, zobacz ikony i ekrany powitalne w aplikacjach.

## Podstawowe elementy konfiguracji

W tym przykładzie przedstawiono domyślne `config.xml` generowane przez CLI `create` polecenia, opisane w interfejs wiersza polecenia:

        <widget id="com.example.hello" version="0.0.1">
            <name>HelloWorld</name>
            <description>
                A sample Apache Cordova application that responds to the deviceready event.
            </description>
            <author email="dev@callback.apache.org" href="http://cordova.io">
                Apache Cordova Team
            </author>
            <content src="index.html" />
            <access origin="*" />
        </widget>
    

Następujące elementy konfiguracji, które pojawiają się w najwyższego poziomu `config.xml` plik i są obsługiwane na wszystkich obsługiwanych platformach Cordova:

*   `<widget>`Element `id` atrybut zawiera identyfikator odwrotnej domeny aplikacji i `version` jego pełna wersja numer wyrażony w notacji z głównych, drobne/patcha.
    
    Tagów widżetu również może mieć atrybuty, które określić alternatywne wersje, a mianowicie versionCode dla Android i CFBundleVersion dla iOS. Zobacz sekcję dodatkowe wersji poniżej szczegóły.

*   `<name>`Element określa Nazwa aplikacji, jak pojawia się na ekranie urządzenia w sklepie app interfejsy.

*   `<description>`i `<author>` określić elementy metadanych i informacji kontaktowych, które mogą pojawić się w ramach oferty app-store.

*   Opcjonalny `<content>` element definiuje wyjścia strony aplikacji w katalogu aktywów sieci web najwyższego poziomu. Wartością domyślną jest `index.html` , który zwyczajowo pojawia się w projekcie na najwyższym poziomie `www` katalogu.

*   `<access>`elementy zdefiniować zestaw aplikacji jest możliwość komunikowania się z zewnętrznych domen. Domyślna wartość powyżej pozwala na dostęp do dowolnego serwera. Zobacz przewodnik białej listy domen szczegóły.

*   `<preference>`Znacznik ustawia różne opcje jako pary `name` / `value` atrybuty. Każdej preferencji `name` jest rozróżniana wielkość liter. Wiele preferencje są unikatowe dla platform określonych, wymienionych w górnej części tej strony. W poniższych sekcjach szczegółowo preferencje, które stosuje się do więcej niż jednej platformy.

### Dodatkowe wersji

Zarówno, Android i iOS obsługuje drugiej wersji ciąg (lub numer) oprócz ten widoczny w app Store, [versionCode][2] dla Android i [CFBundleVersion][3] dla iOS. Poniżej znajduje się przykład, który jawnie ustawia versionCode i CFBundleVersion

 [2]: http://developer.android.com/tools/publishing/versioning.html
 [3]: http://stackoverflow.com/questions/4933093/cfbundleversion-in-the-info-plist-upload-error

        <widget id="io.cordova.hellocordova"
          version="0.0.1"
          android-versionCode="7"
          ios-CFBundleVersion="3.3.3">
    

Jeśli alternatywna wersja nie jest określony, należy zastosować następujące wartości domyślne:

        // assuming version = MAJOR.MINOR.PATCH-whatever
        versionCode = PATCH + MINOR * 100 + MAJOR * 10000
        CFBundleVersion = "MAJOR.MINOR.PATCH"
    

## Globalny preferencje

Następujące ustawienia globalne stosuje się do wszystkich platform:

*   `Fullscreen`pozwala ukryć pasek stanu w górnej części ekranu. Wartością domyślną jest `false` . Przykład:
    
        <preference name="Fullscreen" value="true" />
        

## Wielo--platforma preferencje

Następujące preferencje stosuje się do więcej niż jednej platformy, ale nie wszystkie z nich:

*   `DisallowOverscroll`(domyślnie wartość logiczna, `false` ): zestaw `true` jeśli nie chcesz tego interfejsu, aby wyświetlić wszelkie uwagi, gdy użytkownicy przewiń w przeszłości na początku lub na końcu treści.
    
        <preference name="DisallowOverscroll" value="true"/>
        
    
    Stosuje się do Androida i iOS. Na iOS, overscroll gesty przyczyną treści wraca do pozycji wyjściowej. Na Android produkują bardziej subtelny efekt pomyślna wzdłuż górnej lub dolnej krawędzi zawartości.

*   `BackgroundColor`: Zestaw kolor tła aplikacji. Obsługuje następujące trzy bajty czterobajtową wartość szesnastkowa, z pierwszego bajtu, reprezentujący kanał alfa, a standardowe wartości RGB. W tym przykładzie określa niebieski:
    
        <preference name="BackgroundColor" value="0xff0000ff"/>
        
    
    Stosuje się do Androida i BlackBerry. Zastępuje CSS udostępniane na *wszystkich* platformach, na przykład:`body{background-color:blue}`.

*   `HideKeyboardFormAccessoryBar`(domyślnie wartość logiczna, `false` ): zestaw `true` Aby ukryć dodatkowych narzędzi, który pojawia się nad klawiaturą, pomagając użytkowników nawigacji z jednej formy wejścia do innego.
    
        <preference name="HideKeyboardFormAccessoryBar" value="true"/>
        
    
    Stosuje się do iOS i BlackBerry.

*   `Orientation` (ciąg, domyślne ustawienia `default`): pozwala na blokowanie orientacji i uniemożliwić obracanie w odpowiedzi na zmiany orientacji interfejsu. Możliwe wartości są `default`, `landscape` albo `portrait`. Przykład:
    
        <preference name="Orientation" value="landscape" />
        
    
    Dodatkowo można określić wartości specyficzne dla platformy orientacji, jeśli można umieścić element `<preference>` w elemencie `<platform>`:
    
        <platform name="android">
            <preference name="Orientation" value="sensorLandscape" />
        </platform>
        
    
    Ma zastosowanie do Android, iOS, WP8, Amazon ognia systemu operacyjnego i programu Firefox OS.
    
    **Uwaga**: `default` wartość oznacza Cordova pasek orientacji preferencji wpisu z pliku manifestu/konfiguracja platformy umożliwiające platformie do powrotu do jego domyślne zachowanie.

"domyślne" pozwala zarówno portret i krajobraz tryb - dopiero po realizacji wywołania zwrotnego. I może być może ponownie słowo to w następujący sposób:

Dla iOS orientację można programowo kontrolowane definiując wywołania zwrotnego javascript na okna:

    /** 
    * @param {Number} degree - UIInterfaceOrientationPortrait: 0, UIInterfaceOrientationLandscapeRight: 90, UIInterfaceOrientationLandscapeLeft: -90, UIInterfaceOrientationPortraitUpsideDown: 180
    * @returns {Boolean} Indicating if rotation should be allowed.
    */
    function shouldRotateToOrientation(degrees) {
         return true;
    }
    

## *Funkcja* elementu

Jeśli używasz CLI do tworzenia aplikacji, należy użyć polecenia `plugin` , aby włączyć urządzenie API. To nie modyfikować plik najwyższego poziomu pliku `config.xml` , więc element `< feature >` nie stosuje się do pracy. Jeśli pracy bezpośrednio w SDK i przy użyciu pliku platformy plik `config.xml` jako źródło, należy użyć tagu `< feature >` włączyć urządzenie na poziomie API i zewnętrznych wtyczek. Często pojawiają się z wartości niestandardowe pliki specyficzne dla platformy plik `config.xml` . Na przykład Oto jak określić API urządzenia Android projektów:

        <feature name="Device">
            <param name="android-package" value="org.apache.cordova.device.Device" />
        </feature>
    

Oto, jak element jest wyświetlany dla iOS projektów:

        <feature name="Device">
            <param name="ios-package" value="CDVDevice" />
        </feature>
    

Zobacz API Reference szczegółów w jaki sposób określić każdej funkcji. Zobacz przewodnik rozwoju Plugin, aby uzyskać więcej informacji na wtyczki.

## *Platform* Element

Podczas tworzenia aplikacji za pomocą CLI, czasem jest konieczne do określenia preferencji lub inne elementy specyficzne dla konkretnej platformy. Element `<platform>` umożliwia określenie konfiguracji, które powinny być wyświetlane tylko w jednej platformy `plik config.xml` pliku. Na przykład Oto jak określić, że tylko android należy użyć preferencji pełny ekran:

        <platform name="android">
            <preference name="Fullscreen" value="true" />
        </platform>