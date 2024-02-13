### CI pipeline for Test service

On pull request opened :

1. Testing the test service application (twice)

On pull request merged :

1. Testing the test service application (twice)
2. Build a Docker image
3. Push Docker image to Azure ACR. The image repository name is `psi-test-service` The image tag set as `1.{github.run_number}` - the number of the workflow call (it is incremented by 1 during each workflow call)
