# Rapport för WebbteknikII_Labb 2
EJ222PJ
Eric Jennerstrand 

## Säkerhetsproblem

#### Inte Hashade Lösenord!
Lösenord ska alltid vara hashade i en databas, men i denna applikationen sparas lösenorden i klartext. Detta gör att om databasen bilr hackad får hackaren tillgång till alla lösenord och emailadresser. Om en användare då har samma lösenord på flera sajter har hackaren tillgång till de sajterna också. [1]

#### SQL-injections
Det är möjligt vid inloggningen att göra ett så kallat "SQL-injection", det innebär att man inte behöver skriva rätt mail eller lösenord. Det går att skicka en sql fråga som tex 
" ' OR '1'='1 " och man kommer att bli inloggad för applikationen tror att det är en giltig inloggning. Detta är inte bara dåligt för att man kan logga in utan giltig inloggning utan det går även att använda denna metoden för att förstöra eller ändra data och det skulle även gå att ta bort hela databasen. [2]

#### Nedladdningsbar Databas
Det går att ladda ner databasen, vilket medför en riktigt stor risk för alla användare. Med tanke på att man får full tillgång till alla användaruppgifter och meddelanden. Klienten har också ett krav på att alla meddelanden ska vara oåtkomliga för de som inte har inloggningsuppgifter. Detta kravet uppfylls inte när det går att ladda ner hela databasen. 

#### JavaScript i meddelanden
Det finns inget som hindrar en användare att göra en XSS attack genom att tillexempel göra en knapp eller länk i ett meddelande som gör en redirect till en annan sida där en elak användare kan spara knapptryckarens cookie och sen använda den för att logga in i knapptryckarens identitet. [3]

#### Dålig sessions hantering
När en användare loggar ut förstörs inte sessionen vilket innebär att det går att använda backåtknappen eller skriva in en url som används när man är inloggad för att bli inloggad på samma profil igen. Detta medför att användare 1 kan logga ut och sedan kan användare 2 börja använda datorn och logga in igen på användare 1s profil. [4]

##Prestandaproblem



## Referenser 
[1] "OWASP Password Storage Cheat Sheet" [Online] Tillgänglig: https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet
[Hämtad: 30 november 2015]

[2] "OWASP Top Ten Project A1" [Online] Tillgänglig: https://www.owasp.org/index.php/Top_10_2013-A1-Injection
[Hämtad: 30 november 2015]

[3] "OWASP Top Ten Project A3" [Online] Tillgänglig: https://www.owasp.org/index.php/Top_10_2013-A3-Cross-Site_Scripting_(XSS)
[Hämtad: 30 November 2015]

[4] "OWASP Top Ten Project A2" [Online] Tillgänglig: https://www.owasp.org/index.php/Top_10_2013-A2-Broken_Authentication_and_Session_Management
[Hämtad: 30 November 2015]
