# mitsuba-shapenet

Most ShapeNet models are exported from SketchUp with double-faces. In original Mitsuba renderer without back-face culling, there are black pixels when intersecting the 'back side' face. 

This fork simply modified the 'TriAccel' structure used for ray-triangle intersection. Face normal is used to decide whether the ray could hit the back side.

For more details about mitsuba renderer, please visit its homepage at https://www.mitsuba-renderer.org/ .

And for the dependency of the project, please check https://www.mitsuba-renderer.org/repos/ .

On Windows, you can simply put the dependencies_windows repo under the project folder and rename it as mitsuba-shapenet\dependencies. It would automatically find required headers and libraries.

If you meet the problem of missing header such as mitsuba_precompiled_header.hpp, please turn off MTS_USE_PCH flag during CMake.

There is no vertex normal information included in ShapeNet dataset, so it would cause some rendering issues. For simplicity, you can turn off smooth normal by turning on 'faceNormals' or generating normal by setting 'maxSmoothAngle' in rendering configuration file.

A sample rendering configuration render.xml:

<?xml version="1.0" encoding="utf-8"?>

<scene version="0.5.0">
	<shape type="obj">
		<string name="filename" value="ShapeNetCore.v1/02691156/5903b9eeb53f1f05a5a118bd15e6e34f/model.obj" />
		<boolean name="faceNormals" value="true" />
	</shape>
	
	<emitter type="constant" id="env">
	</emitter>

	<integrator type="bdpt" >
	</integrator>
	
	<sensor type="perspective">
		<transform name="toWorld">
			<lookAt target="0,0,0" origin="1,1,1" up="0,1,0"/>
		</transform>
		<string name="focalLength" value="50mm"/>

		<sampler type="ldsampler">
			<integer name="sampleCount" value="32"/>
		</sampler>

		<film type="ldrfilm">
			<integer name="width" value="600"/>
			<integer name="height" value="600"/>
			<boolean name="banner" value="false"/>
		</film>
	</sensor>
</scene>