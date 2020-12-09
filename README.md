

# Cotation test NP-MOT v0.9

Outil permettant de transformer les ***notes brutes*** du test **NP-MOT** en ***écarts-types*** et en ***classes***


Téléchargement : [Cotation.ods](https://github.com/buckTarle/Cotation_test_NP_MOT/raw/main/Cotation.ods)



Ce document est conçu pour être ouvert avec **[LibreOffice 7.0.3](https://fr.libreoffice.org/download/telecharger-libreoffice/ "libreOffice 7.0.3")** ( les versions supérieures devraient être supportées )
### Déverouiller le fichier

Par defaut le document est verouillé par mot de passe pour eviter les mauvaises manipulations

Si vous souhaiter le deverouiller cliquez sur : Outil -> Protéger la feuille 
- le mot de passe est "belette"

###  Formules brutes utilisés
#### SPA :
-  EcartType/moy

```
= SI( 				INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ; -2 ; 	
	SI (		ET ( 
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >= ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) 
					) ; -1 ; 
		SI (	ET ( 
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >= ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) - 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <= ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) 
					) ; 0 ;
			SI( ET (			
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 1* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ;
					INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) <= ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) 
					) ; 1 ; 
				SI( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 1 )) >  ( INDIRECT( ADRESSE( 4+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) + 2* INDIRECT( ADRESSE( 5+11*(INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 ))-1) ; 2 + $F$7 ; ; ;"SPA") ) ) ; 2 ; "OUPSI" 
				)
			)
		)
	)
)
```
- Classe :
```
=  CONCAT(   
	SI(      				SIERREUR (   ET   ( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );
												INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 1 ;
		SI(     			SIERREUR (   ET   ( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );
												INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 2 ;    
			SI(    			SIERREUR (   ET   ( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );             
												INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 3 ;     
				SI(   		SIERREUR (   ET   ( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );             
												INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 4 ;      
					SI(   	SIERREUR (   ET   ( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) >= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "^[^—]*" ;  ) );             
												INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 2 )) <= VALEUR.NOMBRE( REGEX( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) ; "[^—]*$" ;  ) ) ) ; 0 ) ; 5 ; " - "       
					)     
				)    
			)   
		)  
	)  
	; " / " ;  
	SI(     			NON( INDIRECT( ADRESSE( 12+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 5 ;   
		SI(    			NON( INDIRECT( ADRESSE( 11+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 4 ;    
			SI( 		NON( INDIRECT( ADRESSE( 10+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 3 ;     
				SI( 	NON( INDIRECT( ADRESSE(  9+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 2 ;      
					SI( NON( INDIRECT( ADRESSE(  8+11*( INDIRECT( ADRESSE( LIGNE() ; COLONNE() - 3 )) -1) ; 2 + $F$7 ; ; ;"SPA") ) = "—" ) ; 1 ; " - " )     
				)
			)   
		)  
	) 
)
```


#### Age 
```
SI( 					C3*12+C4 <  48 ; 0 ;
	SI( 				C3*12+C4 <  58 ; 1 ; 
		SI( 			C3*12+C4 <  69 ; 2 ;
			SI( 		C3*12+C4 <  79 ; 3 ;
				SI( 	C3*12+C4 <  90 ; 4 ; 
					SI( C3*12+C4 < 101 ; 5 ; 6 
					)
				)
			)
		)
	)
)
```




