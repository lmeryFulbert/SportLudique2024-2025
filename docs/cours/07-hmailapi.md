# 07-API Hmail

## Automatiser la création de boite aux lettres avec l’PAI HmailServer

L’objectif est simple, être capable de créer autant de boite aux lettre que nécessaire très rapidement à partir d’une liste d’utilisateurs fournie dans un fichier texte. Le script devra evidement être utilisé sur la machine windows qui héberge le serveur hmail.

Cet exemple de code en PowerShell cré une boitte aux lettre. Il faut évidement l’adapter pour en générer plusieurs d’un coup.

```powershell

#**************************************************
#
#     creation d'un compte de messagerie dans hmailserver	
#
#								Auteur: MERY Ludovic
#
#**************************************************	

	Write-Host " Creation d'un compte dans hMailServer ..."
	
	# This creates a COM object against the hMailServer API
	$hm = New-Object -ComObject hMailServer.Application
	
	#On precise le compte administrateur capable de grer le serveur
	$hm.Authenticate("Administrator", "Azerty1234") | Out-Null
	
	##On precise le suffixe DNS utilisé
	$dnsroot = "test.sportludique.fr"; 
	#Le serveur de messagerie peut heberger plusieurs domaine, on cherche celui renseigné plus haut.
	$hmdom = $hm.Domains.ItemByName($dnsroot)
	#On cré un compte.
	$hmact = $hmdom.Accounts.Add()
	
	#On renseigne les attributs du compte.
	$hmact.Address = "toto@test.sportludique.fr"
	$hmact.Active = $true
	$hmact.IsAD = $false
	$hmact.MaxSize = 100
	$hmact.ADUsername = "toto.tata"
	$hmact.PersonFirstName = "toto"
	$hmact.PersonLastName = "tata"
	
	#Et on oublie pas de sauvegarder
	$hmact.save()
	
	Write-Host "Compte cree...Bravo !"
```