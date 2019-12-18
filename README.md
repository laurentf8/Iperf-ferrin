Compte rendu TD IPERF 
===


## Auteur : Laurent FERRIN

# 1   Installation de l’environnement de test

## On teste les commande Iperf

Voici le résultat de la commande:
iperf -c 10.255.255.200 -u -b 3M


    Client connecting to 10.255.255.200, UDP port 5001
    Sending 1470 byte datagrams, IPG target: 3738.40 us (kalman adjust)
    UDP buffer size:  208 KByte (default)
    [  3] local 10.214.15.1 port 35664 connected with 10.255.255.200 port 5001
    [  3] WARNING: did not receive ack of last datagram after 10 tries.
    [ ID] Interval       Transfer     Bandwidth
    [  3]  0.0-10.0 sec  3.75 MBytes  3.15 Mbits/sec
    [  3] Sent 2675 datagrams
    root@214-15:/home/test# 



## On teste le script simule.sh


    root@214-15:/home/test/Documents/Iperf# ./simule.sh 10.12.0.1 10.12.0.2
    No command specified, using /bin/sh
    #ip a
    1: lo: <LOOPBACK> mtu 65536 qdisc noop state DOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    13: veth-server@if12: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether f6:5b:65:4e:a3:10 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 10.12.0.1/24 scope global veth-server
       valid_lft forever preferred_lft forever
    inet6 fe80::f45b:65ff:fe4e:a310/64 scope link 
       valid_lft forever preferred_lft forever
 

# 2  Réalisation des graphes "xy"
    
    
1)
On Lance le serveur avec cette commande:

    root@214-15:/home/test/Documents/Iperf# ./simule.sh 10.12.0.1 10.12.0.2 'iperf -B 10.12.0.1 -s'
    Server listening on TCP port 5001
    Binding to local address 10.12.0.1
    TCP window size: 85.3 KByte (default)

  
    
2)

Pour lancer le client:
    
      root@214-15:/home/test/Documents/Iperf# iperf -c 10.12.0.1

    Client connecting to 10.12.0.1, TCP port 5001  
    TCP window size: 85.0 KByte (default)

    [  3] local 10.12.0.2 port 39224 connected with 10.12.0.1 port 5001
    [ ID] Interval       Transfer     Bandwidth
    [  3]  0.0-10.0 sec   270 MBytes   226 Mbits/sec
  
    


# Les graphiques 


Voici un graphique ou l'on voit sur l'axe des abscisses le delay mis sur le réseaux et en ordonnées le Bandwidth en Mbits/s
![](https://i.imgur.com/OqPWy74.png)

La bande passante diminue car il y a de nombreux paquet qui veulent traverser le réseaux donc "nos" paquets mettent plus de temps à arriver.

</br>    
</br>    
</br>    



Sur le graphique suivant on voit le Bandwidth en fonction de loss

![](https://i.imgur.com/zq099ZM.png)

On à des pertes sur le réseaux et comme on est en TCP on va rémettre les paquet perdu cela génère du trafic et réduit la bande passante disponible.

</br>    
</br>    
</br>    



Voici un graph ou l'on a le pourcentage de duplication en abscisse et la bande passante en ordonnée (Gbits/s)
![](https://i.imgur.com/ug0GFYw.png)
    
En augmentant la duplication des paquet on n'affecte pas la bande passante.
Sa variation doit être lier au network space.





    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    






