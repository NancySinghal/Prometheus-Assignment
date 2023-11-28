# Prometheus-Assignment
### 1. Export the metrics (like request per second, memory usage, cpu usage etc) in the existing mini project given to Interns

1. request_counter = Counter('flask_requests_total', 'Total number of requests received')
    This line creates a Prometheus Counter named flask_requests_total with the description 'Total number of requests received'.
    A Counter is a metric that represents a cumulative count that only goes up.

2. cpu_usage = Gauge('flask_cpu_usage_percent', 'CPU usage percentage')
    This line creates a Prometheus Gauge named flask_cpu_usage_percent with the description 'CPU usage percentage'.
     A Gauge is a metric that represents a single numerical value that can go up or down.

3. @app.route('/metrics')
    def metrics():
      cpu_percent = psutil.cpu_percent()
      cpu_usage.set(cpu_percent)
      return generate_latest(REGISTRY)
   
    When you access the /metrics route of the Flask app, it updates the CPU usage metric and returns a response with all the registered 
    metrics in a format that Prometheus can scrape and collect. This is the endpoint that Prometheus is configured to scrape in order to monitor the Flask app.

4. @app.route('/')
    def home_page():
      request_counter.inc()
      return render_template('index.html')

   Every time someone accesses the main page of the Flask app, the request_counter is incremented, and the content of the 'index.html' template
   is rendered and sent as the response.

### 2. Install Prometheus and Grafana using Docker (with docker-compose)

1. Run - docker compose up -d
2. Now you can access prometheus at http://localhost:9090
   
    ![Screenshot from 2023-11-28 11-54-57](https://github.com/NancySinghal/Prometheus-Assignment/assets/78351041/8e387c5d-3d89-4d1f-b0a6-d45c07c50833)
       
4. And Grafana at http://localhost:3000
    
   ![Screenshot from 2023-11-28 11-56-35](https://github.com/NancySinghal/Prometheus-Assignment/assets/78351041/154a0660-f9ad-45a5-8e48-52380d39620c)

5. Login to Grafana using the credentials provided in environment section of grafana in docker-compose.yml

   ![Screenshot from 2023-11-28 11-57-31](https://github.com/NancySinghal/Prometheus-Assignment/assets/78351041/86254626-7095-40ab-96b7-09243da0322d)


### 3. Configure prometheus (scrape configs) such way that it can scrape the metrics from default metric path of the application job (prometheus.yml)

   ![Screenshot from 2023-11-28 11-57-58](https://github.com/NancySinghal/Prometheus-Assignment/assets/78351041/0e6a4e77-06ad-498a-b0b3-fba6158e0f20)


### 4. Validate the entire configuration to check if the data is coming or not in Prometheus UI

  ![Screenshot from 2023-11-28 11-59-06](https://github.com/NancySinghal/Prometheus-Assignment/assets/78351041/3deb64e3-ba31-4224-a2d4-1e1e5b8b74bc)

### 5. Create the Dashboards in Grafana on top of the metrics exported by adding the Prometheus as a Datasource.

1. For 'Total number of requests received' -> flask_requests_total

    ![Screenshot from 2023-11-28 12-01-53](https://github.com/NancySinghal/Prometheus-Assignment/assets/78351041/49d12d4a-8843-43e9-a221-d00eb76fb12f)

2. For 'CPU usage percentage' -> flask_cpu_usage_percent

    ![Screenshot from 2023-11-28 12-02-15](https://github.com/NancySinghal/Prometheus-Assignment/assets/78351041/14bdff90-c9a4-41f7-87c3-7e7117e6c4bd)

   
