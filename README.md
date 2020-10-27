Export Hybrid Azure AD Join Computer Certificates Report (Updated)
==================================================================

            

WARNING: Due to retirement of Technet Script Gallery, migrated to:


[https://github.com/zjorz/Public-AAD-Scripts/blob/master/Export-ADSyncToolsHybridAzureADjoinCertificateReport.ps1](https://github.com/zjorz/Public-AAD-Scripts/blob/master/Export-ADSyncToolsHybridAzureADjoinCertificateReport.ps1)


 


This script was originally posted here: [https://gallery.technet.microsoft.com/scriptcenter/Export-Hybrid-Azure-AD-f8e51436](https://gallery.technet.microsoft.com/scriptcenter/Export-Hybrid-Azure-AD-f8e51436)


I updated it support a complete AD domain and an AD forest, if that AD forest has multiple AD domains.


For more information please see: [https://jorgequestforknowledge.wordpress.com/2019/10/08/synched-computers-devices-being-cleaned-up-from-azure-ad/](https://jorgequestforknowledge.wordpress.com/2019/10/08/synched-computers-devices-being-cleaned-up-from-azure-ad/)


-


This script generates a report about certificates stored in Active Directory Computer objects, specifically, certificates issued by the Hybrid Azure AD join feature.


It checks the certificates present in the UserCertificate property of a Computer object in AD and, for each non-expired certificate present, validates if the certificate was issued for the Hybrid Azure AD join feature (i.e. Subject Name matches CN={ObjectGUID}).


Before, Azure AD Connect would synchronize to Azure AD any Computer that contained at least one valid certificate but starting on Azure AD Connect version 1.4, the synchronization engine can identify  Hybrid Azure AD join certificates and will ‘cloudfilter’
 the computer object from synchronizing to Azure AD unless there’s a valid Hybrid Azure AD join certificate.


Azure AD Devices that were already synchronized to AD but do not have a valid Hybrid Azure AD join certificate will be deleted (CloudFiltered=TRUE) by the sync engine.


 


--> Looking at a specific computer


.\Export-ADSyncToolsHybridAzureADjoinCertificateReport.ps1 -DN 'CN=Computer1,OU=SYNC,DC=Fabrikam,DC=com'


 


--> Looking at computer objects within a specific OU


.\Export-ADSyncToolsHybridAzureADjoinCertificateReport.ps1 -DN 'OU=SYNC,DC=Fabrikam,DC=com' -Filename 'MyHybridAzureADjoinReport.csv' -Verbose


 


--> Looking at computer objects within a specific AD domain


.\Export-ADSyncToolsHybridAzureADjoinCertificateReport.ps1 -DN 'DC=child,DC=Fabrikam,DC=com' -Filename 'MyHybridAzureADjoinReport.csv' -Verbose


 


--> Looking at computer objects within a specific AD forest


.\Export-ADSyncToolsHybridAzureADjoinCertificateReport.ps1 -DN PhantomRoot -Filename 'MyHybridAzureADjoinReport.csv' -Verbose


-


For any questions or feedback use the Q&A of the script AND send me an e-mail through the following link: [Questions/Feedback](mailto:Jorge's Script Gallery <scripts.gallery@iamtec.eu>?subject=[Script Gallery Feedback:] 'REPLACE-THIS-PART-WITH-SOMETHING-MEANINGFULL')


 


 


 

 

        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
