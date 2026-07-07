# 27. Komunikaty ICMP, rodzaje, usługi wspierane poprzez protokół ICMP.

ICMP (Internet Control Message Protocol) to protokół warswy sieciowej modelu
OSI, wykorzystywania do diagnostyki sieci (komenda ping) oraz trasowania
(wyznaczania trasy komunikacji pomiędzy węzłami sieci, komenta traceroute).

ICMP może przekazać kilka typów wiadomości. Najczęstszymi z nich są:
* echo request (wysyłany za pomocą ping)
* echo reply (odpowiedź na echo request)
* destination unreachable (po drodze do węzła o danym adresie napotkano
krytyczny problem uniemożliwiający połączenie się z nim)
* time exceeded (rządanie przekroczyło maksymalny dozwolony czas na spełnienie)
* traceroute (rządanie śledzenia trasy do danego węzła w sieci)
* redirect message (zmiana trasowania)
