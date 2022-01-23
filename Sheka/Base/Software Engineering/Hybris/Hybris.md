03.05.2021  15:25
Tags:  |
____

## Hybris
Hybris is e commerce solution.
Hybris is multy channel ecommerce and Product managment software.

Competitors of Hybris:
Oracle - ATG
OPen Source - Magento
IBM - WebSphere Commerce

Java --> Project - write code
Hybris -- Extensions - We write code

Hybris is a Omni channel Commerce Solutions.
Example of Omni channel:
start researching on Website .. see multiple options on Website. You select one of product and buy it, modify address, apply a voucher, you multiple options to pay, select one of Payment, place an Order, return as well.

Hybris version:
5.4.3.2
major feature minor patch

Key concepts of Spring:
1. Dependency Injection
2. AOP
3. Spring MVC
4. Spring Security

##  Hybris b2c installation
1. извлекать архив c помощью 7-zip
2. \installer
3. install.bat -r b2c_acc_plus
4. \hybris\bin\platform
5. ant modulegen -Dinput.module=accelerator -Dinput.name=training -Dinput.package=de.hybris.training -Dinput.template=develop
6. change C:\Users\sheka\Desktop\hybrisTutorial\HYBRISCOMM180800P_8-70003534 (1)\hybris\config\localextensions.xml
7. C:\Users\sheka\Desktop\hybrisTutorial\HYBRISCOMM180800P_8-70003534 (1)\hybris\config\local
8. website.electronics.http=http://electronics.local:9001/trainingstorefront
website.electronics.https=https://electronics.local:9002/trainingstorefront
website.apparel-uk.http=http://apparel-uk.local:9001/trainingstorefront
website.apparel-uk.https=https://apparel-uk.local:9002/trainingstorefront
website.apparel-de.http=http://apparel-de.local:9001/trainingstorefront
website.apparel-de.https=https://apparel-de.local:9002/trainingstorefront
8. C:\Windows\System32\drivers\etc
9. 127.0.0.1 localhost electronics.local apparel-uk.local apparel-de.local
10. ant initialize
##  ant all vs ant clean all


____ 
### Links
-