a. Go to the Agent node, and fetch a JWT SVID, /opt/spire-agent/bin/spire-agent api fetch jwt -audience mys3 -socketPath /opt/spire-agent/sockets/agent.sock This should give a response like


b. Select the actual JWT from the output, and save it in a file.  We'll call it "token" in this case. 
   
c. Call the AWS API for the S3 bucket, using the role you created and the path to the token file in environmental variables.  There are many permutations on how this can be done.  This functionality is available in the various AWS SDKs.