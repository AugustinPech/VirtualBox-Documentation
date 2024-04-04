```mermaid
---
title : Les composants d'internet
---
graph LR
	A[ navigateur ]
    B(( Apache
    NginX))
    D(( D ))
    F(( F ))
    H([someting
    else])
    I(( I ))
    L[ navigateur ]
    PHP[ PHP ]
    BDD[( BDD )]
    ADMIN[ PHP My
    Admin ]
    b[[ FAI ]]
    a[[ FAI ]]
    OS1<-->M
    OS2<-->M
    D<-->H
    B<-->a<-->F
    B<-->PHP
    PHP<-->BDD
    PHP<-->ADMIN
    M<-->N
    N-->b-->I
    I<-->F
    F<-->D
    I<-->D

    subgraph Real physical place somewhere
        subgraph User1
            A<-->OS1
        end
        subgraph User2
		    L<-->OS2
        end
        M[switch]
        N[router]
	end
    subgraph server
        subgraph OS server
            subgraph serveur WEB
		        B
                PHP
                BDD
                ADMIN
            end
        end
	end
    subgraph internet
        D
        F
        I
	end

    
style A stroke-width:2px,stroke-dasharray: 5 5
style B stroke-width:2px,stroke-dasharray: 5 5
style L stroke-width:2px,stroke-dasharray: 5 5
```
****
```mermaid
---
title : FAI 
---
  graph LR
    subgraph Real physical place somewhere
      subgraph U1[ User1 ]
        UIP1[Private IP
        192.168.8.174]
      end
      subgraph U2[User2]
        UIP2[Private IP
        192.168.8.xxx]
      end
      subgraph G[Routing bay]
        switch
        subgraph IPP[gateway]
          GWIP1[listening IP
          192.168.8.254]
          GWIPP[public IP
          185.79.148.1]
        end
        ROUTER
      end
    end
    subgraph legend
        IPPrivate[private IP]
        IPPublic[public IP]
    end
    GWIPP-->ROUTER
    ROUTER --> OUT[the WEB wilderness]
    GWIP1 --> GWIPP
    UIP2 -- adress MAC--> switch
    UIP1 -- adress MAC--> switch-- adress MAC--> GWIP1
    style UIP1 fill:#f9f
    style UIP2 fill:#f9f
    style GWIP1 fill:#f9f
    style IPPrivate fill:#f9f
    style IPPublic fill:#f96
    style GWIPP fill:#f96
```

## Tests de connectivité et chemins
|      Commande      |                      Utilisation                       | Exemples               |
| :----------------: | :----------------------------------------------------: | ---------------------- |
|       `ip a`       | présente les cartes réseaux et leurs IP sur la machine | ![alt text](image.png) |
| `whois domaine.xx` |            traduit un IP en nom de domaine             | `whois 88.198.21.14`   |
|     `nslookup`     |            traduit un nom de domaine en IP             | `whois google.fr`      |
|       `host`       |                   DNS Lookup utility                   |                        |
|    `traceroute`    | trace la route vers un IP ou un nom de domaine |                        |