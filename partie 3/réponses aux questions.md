- Lors de la création d’une interface réseau, virtualBox propose les choix suivantes :

- Pour les type d’interface suivantes, faites un dessin pour expliquer comment est connectée la machine virtuelle à ce réseau. 
    ****
    ```mermaid
    ---
    title : Interface NAT
    ---
        graph LR
        subgraph VB[VBox app]
            VM1
            VM2
            VMN
        end
        subgraph VM's host

                N1[NAT]
                N2[NAT]
                N3[NAT]
                PNIC[Physical
                    Network
                    Interface
                    Card
                    ]
        end
        VM1-->N1
        VM2-->N2
        VMN[VM...]-->N3

        N1-- One way-->PNIC
        N2-- One way-->PNIC
        N3-- One way-->PNIC
        linkStyle 3,4,5 stroke:green, stroke-dasharray: 5 5
        PNIC --> ROUTER[physical
                        router
                        ]
        ROUTER--> OUT[out there
                    on the 
                    internet]
    ```
    L'interface NAT ne permet pas de prendre le controle depuis le HOST vers le GUEST. Elle permet uniquement les sortie depuis le GUEST vers l'extérieur.
    ****
    ```mermaid
    ---
    title : Bridged Adapter
    ---
    graph LR

    subgraph VM's host
        subgraph IP[Bridge adapter :]
            RealIP
            VIP1
            VIP2
            VIP3[VIP...]
        end
            RealIP-->PNIC[Physical
                Network
                Interface
                Card
                ]
    end
        subgraph VB[VBox app]
            VM1-->VIP1
            VM2-->VIP2
            VMN[VM...]-->VIP3
        end

    PNIC --> ROUTER[physical
                    router
                    ]
    ROUTER--> OUT[out there
                on the 
                internet]
    linkStyle 0 stroke:green, stroke-dasharray: 5 5

    style IP text-align:left;

    ```
    La Vm est branchée 'comme en vrai' sur internet.
    Elle est visible sur le réseau par les autres utilisateurs comme si c'était une vraie machine.
    ****
    ```mermaid
    ---
    title : Host-only Adapter
    ---
        graph LR
        subgraph VB[VBox app]
            VM1
            VMN[VM...]
        end
        subgraph VM's host

                PNIC[Physical
                    Network
                    Interface
                    Card
                    ]
                DHCP[Dynamic
                    Host
                    Config
                    Protocol
                    ]
        end

        DHCP--gives IP -->VM1--netplan asks for IP-->DHCP
        DHCP--gives IP-->VMN[VM...]--netplan asks for IP-->DHCP

        PNIC --host only --> ROUTER[physical
                        router
                        ]
        ROUTER--> OUT[out there
                    on the 
                    internet]

    ```
    Dans un interface Host Only on a une connexion des virtualBox vers le Host uniquement. Elles ne se voient pas entre elles.
    ****
## Vous devriez pouvoir répondre à :
- C’est quoi un VM ? A quoi ca sert ?

    une **Virtual Machine** est une simulation d'une machine (ici : d'un ordinateur).
    C'est un outil qui permet de simuler des configurations et des actions sur ces config sans prendre trop de risques. On peut eussi copier, supprimer , modifier très facilement ces machines.
- C’est quoi un Guest Operating Systems ?, un Host operating Systems ?

    le **GOS** est l'**OS** de la VM

    le **HOS** est l'**OS** de la machine physique, l'hôte
- Quels sont les options pour configurer l’interface réseau ?

    NAT // Bridge Adapter // Host-only Adapter
- Que signifie NAT ?
    
    Network Address Translation
- A quoi ca sert ?
    
    Dans notre cas l'interface NAT rend routable les machines virtuelles.
    L'interface fait correspondre des adresses IPs privées non routable à une addresse routable.
    ****
- Comment fait- on pour se connecter sur un serveur avec une carte réseau configuré avec un NAT ?

    on ne peut pas 
- Comment faire pour avoir plusieurs interfaces au sein de la VM ?

    il faut créer d'autres virtual NIC sur la config de la VM
- A quoi ca sert ?

    à avoir différents types de connections qui permettent d'accéder au server par différents chemins.
- A quoi ca sert les VirtualBox Guest Additions ?

    ça sert à rajouter des périfériques partagés entre le HOST et le GUEST
- Comment ca s’installe ?

    J'ai fait une doc d'instal'.