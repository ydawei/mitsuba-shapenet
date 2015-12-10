# mitsuba-shapenet

Most ShapeNet models are exported from SketchUp with double-faces. In original Mitsuba renderer without back-face culling, it would produce black pixels when intersecting on the 'back side' face.  
