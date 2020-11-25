FROM pritt/opencv-small:latest

# Download dataset
RUN echo "\n\n------------------------------------------> Download of YACCLAB reduced datasets" && \
wget https://imagelab.ing.unimore.it/files/YACCLAB_dataset3D_reduced.zip -O dataset.zip && \
unzip -qq dataset.zip && \
rm dataset.zip  && \
wget imagelab.ing.unimore.it/files/YACCLAB_dataset_reduced.zip -O dataset.zip && \
unzip -qq dataset.zip && \
rm dataset.zip  && \
echo "------------------------------------------> DONE!"