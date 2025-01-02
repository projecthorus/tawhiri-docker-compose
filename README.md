Requirements
===

- Roughly 10GB of free space
- Docker and Docker compose (v2.32.1 or higher)
- Will not run on a mac due to mmap - OSError: [Errno 12] Cannot allocate memory

Running
===

1. Modify docker-compose if customization is required (default port is 8000, thread and worker count suitable for a medium sized instance)
2. Run `docker compose up`
3. The downloader will take some time to download the wind model and DEM - from Australia this takes about 30 minutes
4. Test the api
```sh
curl "http://localhost:8000/api/v1/?launch_latitude=10&launch_longitude=10&launch_datetime=$(python3 -c 'import datetime; print(datetime.datetime.now().strftime("%Y-%m-%dT%H:%M:%SZ"), end="")')&launch_altitude=0&ascent_rate=5.00&burst_altitude=1000&descent_rate=5.28"
```
5. If docker volumes are to be persisted see note below about disabling the initial downloader and dem/ruaumoko download


Notes
===
- Every `docker compose up` performed will trigger a dem and wind model download before starting tawhiri. Once an initial model and dem is downloaded you can comment out the `downloader` and `ruaumoko` services, along with references to them in `depends` sections.