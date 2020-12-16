

# Cotation test NP-MOT v1.0

Outil permettant de transformer les ***notes brutes*** du test **NP-MOT** en ***écarts-types*** et en ***classes***


Téléchargement : [Cotation.ods](https://github.com/buckTarle/Cotation_test_NP_MOT/raw/main/Cotation.ods)



Ce document est conçu pour être ouvert avec **[LibreOffice 7.0.3](https://fr.libreoffice.org/download/telecharger-libreoffice/ "libreOffice 7.0.3")** ( les versions supérieures devraient être supportées )
### Déverouiller le fichier

Par defaut le document est verouillé par mot de passe pour eviter les mauvaises manipulations

Si vous souhaiter le deverouiller cliquez sur : Outil -> Protéger la feuille 
- le mot de passe est "belette"

###  Formules simplifiés

DS( sigma ) :

| [ -oo ; -2DS ] | ] -2DS ; -1DS ] | ] -1DS ; +1DS [ | [ +1DS ; +2DS [ | [ -2DS ; +oo ] |
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  -2 | -1 | 0 | +1 | +2 |

###  Formules brutes utilisés
#### TON
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"TON") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
- Classe :
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"TON") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### MOT 
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"MOT") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
- Classe :
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"MOT") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### LAT
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"LAT") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
-  Classe : 
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"LAT") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### PRA
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"PRA") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
-  Classe : 
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"PRA") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### GNO
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"GNO") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
-  Classe : 
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"GNO") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### HAB
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"HAB") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
-  Classe : 
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"HAB") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### SPA :
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
- Classe :
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### RYT
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"RYT") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
-  Classe : 
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"RYT") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### ATT
-  EcartType/moy : 
```
= SI( 					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ; -2 ; 	
	SI (		ET ( 		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ) ; -1 ; 
		SI (	ET (		INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) > ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ) ; 0 ;
			SI( ET (	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) < ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ) ; 1 ; 
				SI( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >=  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"ATT") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
-  Classe : 
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "^[^—]*" ;  ) );
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( 	INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "^[^—]*" ;  ) );             
									INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     				NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) = "—" ) ; 5 ;   
		SI(    				NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) = "—" ) ; 4 ;    
			SI( 			NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) = "—" ) ; 3 ;     
				SI( 		NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) = "—" ) ; 2 ;      
					SI( 	NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"ATT") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```
#### Age 
```
SI( 						C3*12+C4 <  48 ; 0 ;
	SI( 					C3*12+C4 <  58 ; 1 ; 
		SI( 				C3*12+C4 <  69 ; 2 ;
			SI( 			C3*12+C4 <  79 ; 3 ;
				SI( 		C3*12+C4 <  90 ; 4 ; 
					SI( 	C3*12+C4 < 101 ; 5 ; 6 
					)
				)
			)
		)
	)
)
```




