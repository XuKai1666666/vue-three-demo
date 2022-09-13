<script setup lang="ts">
import Keli from './keli.vue';
const modelData={
    "uuid": "1",
    "name":"可莉",
    "url":"src/assets/keli/可莉2.0.pmx",
    "model": {
        "coordinate": {
            "x": 90,
            "y": -50,
            "z": -50,
            "scale": 3,
        },
        
    },
}
const uuid=modelData.uuid;
const name=modelData.name;
const modelCoordinateX=modelData.model.coordinate.x
const modelCoordinateY=modelData.model.coordinate.y
const modelCoordinateZ=modelData.model.coordinate.z
const modelCoordinateScale=modelData.model.coordinate.scale
const url=modelData.url
</script>
<template>
    <Keli 
    :uuid="uuid"
    :name="name"
    :modelCoordinateX="modelCoordinateX"
    :modelCoordinateY="modelCoordinateY"
    :modelCoordinateZ="modelCoordinateZ"
    :modelCoordinateScale="modelCoordinateScale"
    :url="url"
    />
</template>