This package is used to access SuperstaQ via a Web API through Qiskit. Qiskit programmers
can take advantage of the applications, pulse level optimization, and write-once-target-all
features of SuperstaQ.


Please note that Python version `3.7` or higher is required. qiskit-superstaq and all of its
dependencies can be installed via:

```
git clone https://github.com/SupertechLabs/qiskit-superstaq.git
cd qiskit-superstaq
conda create -n qiskit-superstaq-env python=3.8
conda activate qiskit-superstaq-env
pip install -r dev-requirements.txt
pip install -e .
```

Make sure to always be in the qiskit-superstaq-env (via ``conda activate qiskit-superstaq-env``) when you're working on qiskit-superstaq.

### Creating and submitting a circuit through qiskit-superstaq
```
import qiskit
import qiskit_superstaq as qss

token = "Insert superstaq token that you received from https://superstaq.super.tech"

superstaq = qss.superstaq_provider.SuperstaQProvider(
    token,
    url=qss.API_URL,
)

backend = superstaq.get_backend("ibmq_qasm_simulator")
qc = qiskit.QuantumCircuit(2, 2)
qc.h(0)
qc.cx(0, 1)
qc.measure(0, 0)
qc.measure(1, 1)

print(qc)
job = backend.run(qc, shots=100)
print(job.result().get_counts())
```
