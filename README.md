# Lab 12 runnable Compose examples

All three projects expose the same notes resource and use a separate, project-scoped
PostgreSQL 18 named volume. Choose the Express reference first; FastAPI and NestJS
show the same approach in the other Lab 11 frameworks. The assessed exercise also
requires applying it to your own backend project.

| Folder | Host URL | App container port | Project prefix |
| --- | --- | --- | --- |
| express | http://localhost:8082 | 3000 | lab12-express |
| fastapi | http://localhost:8083 | 8000 | lab12-fastapi |
| nestjs | http://localhost:8084 | 3000 | lab12-nestjs |

Read each project's README before starting. Each Compose file has two services,
app and db, no published database port, an explicit DB readiness check and a named
volume at /var/lib/postgresql. Set a stable student ID in each project's ignored
.env file. For your own project choose another stable project name.

Each project's POST /notes returns the created row; GET /notes returns an array.
Record fields are id, student_id, body and created_at. The health route verifies
an actual SELECT 1 against the database. Error responses intentionally omit
credentials and database connection details.

The Node dependency trees are pinned by package-lock.json. Python direct packages
are pinned in requirements.txt; its transitive dependency tree is not fully locked.
Base tags pin a major/runtime family and follow patch updates rather than an image
digest. These are local teaching examples, not a high-availability deployment.

## Verification

All three projects were built and run on Docker Desktop's Linux engine. Checks
covered actual HTTP POST/GET, input rejection, SQL-looking text stored as data,
a request from inside the app container, independent SQL results, restart,
container removal/recreation with the original row and volume retained, and DB
outage/recovery without replacing the app container. Disposable test containers,
volumes and QA image tags were removed. No online server was changed.

## Optional API test client / เครื่องมือทดสอบ API เสริม

Each downloaded project includes api-testing/ with a bilingual guide, Postman
collection and environment template. The website also offers api-testing.zip.
Use Postman, PowerShell or curl to create one baseline row and compare the same
row after restart and container replacement. This supports existing report
evidence; it adds no new graded task. In a source checkout the shared assets live
at [../api-testing/](../api-testing/API-TESTING.md).

starter ZIP แต่ละชุดมีคู่มือสองภาษาและไฟล์นำเข้า Postman ใน api-testing/ เลือก Postman,
PowerShell หรือ curl ได้ สร้าง baseline ครั้งเดียว แล้ว GET ตรวจแถวเดิมหลัง restart
และสร้างคอนเทนเนอร์ใหม่ เป็นแนวทางเสริมสำหรับหลักฐานเดิม ไม่ใช่งานส่งเพิ่ม
