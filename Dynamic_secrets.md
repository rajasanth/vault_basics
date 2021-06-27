# Enabling AWS secret Engine
vault secrets enable -path=aws aws

# Configure the AWS secrets engine.

vault write aws/config/root \
    access_key=$AWS_ACCESS_KEY_ID \
    secret_key=$AWS_SECRET_ACCESS_KEY \
    region=us-east-1

# Tell Vault to create a role with a name <my-role> with the desired policy attached with All EC2 permissions

vault write aws/roles/my-role \
        credential_type=iam_user \
        policy_document=-<<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1426528957000",
      "Effect": "Allow",
      "Action": [
        "ec2:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
EOF

# Generate the secret
    
    vault read aws/creds/my-role
    
lease_id           aws/creds/my-role/vAGZ071PLGSaTTjUHfZr11Mk
lease_duration     768h
lease_renewable    true
access_key         <access-key>
secret_key         <secret-key>
security_token     <nil>    

# Revoke the secret
    Auto removal of the secret post lease_duration.
 PS C:\Users\212801747> vault lease revoke aws/creds/my-role/vAGZ071PLGSaTTjUHfZr11Mk                                                 All revocation operations queued successfully!
    
