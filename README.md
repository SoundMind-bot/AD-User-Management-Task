$users = @(
    @{Name="Ato"; SamAccountName="ato"; UserPrincipalName="ato@verdantphotostudio.com"},
    @{Name="Yvonne"; SamAccountName="yvonne"; UserPrincipalName="yvonne@verdantphotostudio.com"},
    @{Name="Olajide"; SamAccountName="olajide"; UserPrincipalName="olajide@verdantphotostudio.com"}
)

foreach ($user in $users) {
    New-ADUser -Name $user.Name -GivenName $user.Name -Surname "User" -SamAccountName $user.SamAccountName -UserPrincipalName $user.UserPrincipalName -Path "OU=Users,DC=verdantphotostudio,DC=com" -AccountPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force) -Enabled $true
    Add-ADGroupMember -Identity "Remote Desktop Users" -Members $user.SamAccountName
}
