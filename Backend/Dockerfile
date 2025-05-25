FROM rust:1.87

ENV PATH="/root/.cargo/bin:${PATH}"

WORKDIR /usr/app

COPY . /usr/app

RUN cargo install --path . && \
	cargo install diesel_cli --no-default-features --features postgres

CMD ["/bin/bash", "-c", "diesel migration run && login-app-backend"]
