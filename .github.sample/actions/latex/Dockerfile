FROM paperist/alpine-texlive-ja

RUN apk add bash git jq curl

ADD entrypoint.sh /entrypoint.sh
RUN ["chmod", "+x", "/entrypoint.sh"]
ENTRYPOINT ["/entrypoint.sh"]
