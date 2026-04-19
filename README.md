# 🚀 Java + Docker + Kubernetes (Kind)

This project demonstrates a simple end-to-end DevOps workflow:

* Build a Java application
* Containerize it using Docker
* Deploy it to Kubernetes using Kind

---

## 🧱 Tech Stack

* Java (JDK 17 / 21)
* Docker
* Kubernetes (Kind)
* kubectl

---

## 📂 Project Structure

```
.
├── App.java
├── App.class
├── Dockerfile
├── deployment.yaml
```

---

## ☕ Java Application

A simple Java program:

```java
public class App {
    public static void main(String[] args) {
        System.out.println("Hello DevOps Journey 🚀");
    }
}
```

Compile the code:

```bash
javac --release 17 App.java
```

---

## 🐳 Docker Setup

### Dockerfile

```dockerfile
FROM eclipse-temurin:17-jdk-jammy
WORKDIR /app
COPY App.class .
CMD ["java", "App"]
```

### Build Image

```bash
docker build -t java-app .
```

### Run Container

```bash
docker run java-app
```

---

## ☸️ Kubernetes (Kind)

### Create Cluster

```bash
kind create cluster
```

### Load Local Image into Cluster

```bash
kind load docker-image java-app
```

---

## 🚀 Deployment

### deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: java-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: java-app
  template:
    metadata:
      labels:
        app: java-app
    spec:
      containers:
      - name: java-app
        image: java-app
        imagePullPolicy: Never
```

---

### Apply Deployment

```bash
kubectl apply -f deployment.yaml
```

### Check Pods

```bash
kubectl get pods
```

---

## 🔍 View Logs

```bash
kubectl logs <pod-name>
```

Example output:

```
Hello DevOps Journey 🚀
```

---

## ⚠️ Challenges Faced

* Java version mismatch (compiled with Java 21, ran on Java 17)
* ImagePullBackOff in Kubernetes
* Understanding local Docker vs Kubernetes image environments

---

## 🧠 Key Learnings

* Difference between Image, Container, and Pod
* Kubernetes Deployment → Pods → Containers flow
* Image pull policies (`Never`, `IfNotPresent`, `Always`)
* Why Kubernetes is designed for long-running applications

---

## 🚀 Next Steps

* Convert to Spring Boot application
* Expose application via Kubernetes Service
* Add database (PostgreSQL)
* Implement CI/CD pipeline
* Deploy to cloud (AWS)
---

