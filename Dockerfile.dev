FROM python:3.8-bookworm
ENV FLASK_ENV development

# Set the working directory to /mab_backend
WORKDIR /mab_backend

# Copy the current directory contents into the container at /mab_backend
COPY ./requirements.txt /mab_backend/requirements.txt

# # Install build dependencies
# RUN apt-get update && apt-get install -y build-essential automake libtool

# # Build sqlit3.45
# RUN cd /mab_backend/rag_cahtbot/additions/sqlite-autoconf-3450100 && \
#     ./configure --prefix=/usr/local && \
#     make && \
#     make install

# Install any needed packages specified in requirements.txt
RUN pip3 install --no-cache-dir -r requirements.txt
# RUN pip3 install --no-cache-dir --upgrade pgvector psycopg2-binary
RUN pip3 install better_profanity

# Define environment variable
ENV FLASK_APP run.py

RUN apt-get update && apt-get install ffmpeg libsm6 libxext6  -y

# Run app.py when the container launches
CMD ["flask", "run", "--host=0.0.0.0", "--port=5000"]
