a. Click "Create Role", and select "Web identity"
![Create Web Identity Role](/mavwali/scenarios/spire-oidc/assets/step5a.png)

b. Select the provider and the audience from the pulldown menus
![Role Provider and Audience selection](/mavwali/scenarios/spire-oidc/assets/step5b.png)

c. Select or create policies as needed and associate it with the Role
![Associate Policy to IAM Role](/mavwali/scenarios/spire-oidc/assets/step5c.png)

d. Give the role a name
![Role Name](/mavwali/scenarios/spire-oidc/assets/step5d.png)

e. You'll need to edit the Role to ad the SPIFFE Id.  Select the Role, and then selecSt the "Trust relationships" tag 
![Trust Relationship for Role](/mavwali/scenarios/spire-oidc/assets/step5e.png)

f. Edit the Trust relationship, adding the line "spire-oidc-demo.skitalee.org:sub": "spiffe://spire-oidc-demo.skitalee.org/oidc-test-workload" This restricts the Role to JWT SVIDs with the SPIFFE Id one wants to allow.
![Restrict Role to a SPIFFEID](/mavwali/scenarios/spire-oidc/assets/step5f.png)

g. Verify the new condition. 
![Verify New Condition](/mavwali/scenarios/spire-oidc/assets/step5g.png)