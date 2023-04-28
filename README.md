# NDVI_Himalaya
#to find the area
area=Himalaya_AOI.area().getInfo()/(1000*1000)
print('Area of AOI is:',round(area,2),'Sqkm')
print('perimeter:',Himalaya_AOI.perimeter().divide(1000).getInfo())

#######################################
# Load an image
# image = ee.Image(.................)

# Create an image where each pixel's value is its area in square meters
pixelAreaImage = ee.Image.pixelArea()

# Calculate the total area of the image in square kilometers
totalArea = pixelAreaImage.reduceRegion(
    reducer=ee.Reducer.sum(),
    geometry=Himalaya_AOI,             #image.geometry()
    scale=30,
    maxPixels=1e9
).get('area')

# Convert the result from square meters to square kilometers
totalArea = ee.Number(totalArea).divide(1000 * 1000)

# Print the result
print('Total area:', totalArea.getInfo())
