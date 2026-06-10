# Railway deployment — single process, multi-threaded.
#
# Why --workers 1 --threads 4?
# APScheduler runs inside the Python process at import time.
# --workers 2 would start TWO scheduler instances → duplicate SLA
# notifications every 10 minutes and the backup job running twice daily.
# --threads 4 gives concurrent request handling without a second process.
# Railway's starter plan runs on a shared CPU anyway, so workers > 1
# gives no throughput benefit but doubles the scheduler fire rate.
#
# If you ever scale to --workers 2, also set SCHEDULER_ENABLED=false on
# the second worker via Railway's service environment variables.

web: gunicorn app:app --workers 1 --threads 4 --bind 0.0.0.0:$PORT --timeout 120
