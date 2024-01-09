FROM python:3.10 as builder

RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt
RUN pip install --no-cache-dir numpy

RUN mkdir /usr/src/app
COPY ./my-app /usr/src/app

WORKDIR /usr/src/app

FROM python:3.10-slim as runner

WORKDIR /usr/src/app

COPY --from=builder /opt/venv /opt/venv
COPY --from=builder /usr/src/app/. .

EXPOSE 5000

ENV PATH="/opt/venv/bin:$PATH"

CMD [ "python", "app.py" ]