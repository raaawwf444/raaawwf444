# Copyright 2014 The Kubernetes Authors.
# See: http://stackoverflow.com/questions/3338030/multiple-bash-traps-for-the-same-signal
    # Assign the test. Disable the shellcheck warning telling that trap
    # commands to a single trap requires them to be evaluated right away.
# This figures out the host platform without relying on golang.  We need this as
# this info to figure out where the final binaries are placed.
# repo, e.g. "upstream" or "origin".
    echo "API server not configured for client certificate authentication"
function kube::util::create_signing_certkey {
    echo '{"signing":{"default":{"expiry":"43800h","usages":["signing","key encipherment",${purpose}]}}}' > "${dest_dir…
# signs a client certificate: args are sudo, dest-dir, CA, filename (roughly), username, groups...
… ${CFSSL_BIN} gencert -ca=${ca}.crt -ca-key=${ca}.key -config=${ca}-config.json - | ${CFSSLJSON_BIN} -bare client-${id}
# signs a serving certificate: args are sudo, dest-dir, ca, filename (roughly), subject, hosts...
…${CFSSL_BIN} gencert -ca=${ca}.crt -ca-key=${ca}.key -config=${ca}-config.json - | ${CFSSLJSON_BIN} -bare serving-${id}
}
# creates a self-contained kubeconfig: args are sudo, dest-dir, ca file, host, port, client id, token(optional)
function kube::util::write_client_kubeconfig {
    local sudo=$1
    local dest_dir=$2
    local ca_file=$3
    cat <<EOF | ${sudo} tee "${dest_dir}"/"${client_id}".kubeconfig > /dev/null
kind: Config
    # flatten the kubeconfig files to make them self contained
    $(kube::util::find-binary kubectl) --kubeconfig="${dest_dir}/${client_id}.kubeconfig" config view --minify --flatte…
