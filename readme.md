# Ray run jobs
Ray Job Submission can be used to submit Ray programs to your Ray cluster. To do this, you must be able to access the Ray Dashboard, 
which runs on the Ray head node on port 8265. One way to do this is to port forward 127.0.0.1:8265 on your local machine to 127.0.0.1:8265 
on the head node using the Kubernetes port-forwarding command.

```bash
kubectl -n ray port-forward service/example-cluster-ray-head 8265:8265
```

Then in a new shell, you can run a job using the CLI:

```bash
export RAY_ADDRESS="http://127.0.0.1:8265"

ray job submit --runtime-env-json='{"working_dir": "./", "pip": ["requests==2.26.0"]}' -- "python script.py"
```
