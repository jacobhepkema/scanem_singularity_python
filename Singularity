Bootstrap: docker

From: continuumio/miniconda3

%files
    environment.yml

%post
    apt-get update && apt-get install -y --no-install-recommends apt-utils build-essential make zlib1g
    apt-get update && apt-get install -y procps
    
    ENV_NAME=$(head -1 environment.yml | cut -d' ' -f2)
    echo ". /opt/conda/etc/profile.d/conda.sh" >> $SINGULARITY_ENVIRONMENT
    echo "conda activate $ENV_NAME" >> $SINGULARITY_ENVIRONMENT
    
    . /opt/conda/etc/profile.d/conda.sh
    # create environment
    conda env create -f environment.yml -p /opt/conda/envs/$ENV_NAME
    
%runscript
    exec /opt/conda/envs/$(head -n 1 environment.yml | cut -f 2 -d ' ')/bin/"$@"
