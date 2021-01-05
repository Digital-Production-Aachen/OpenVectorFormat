# OpenVectorFormat

A format description based on Google protobuf. The format is used for controlling a laser in combination with a galvanometer scanner. It supports multi scanfield arrays as well as additional machine axis controls.

## Basic Object Model

The basic object model of the Open Vector Format is derived from the layer wise build up process of additive manufacturing processes. 
The most basic data object types and their relationships can be found in FIG. 2. In this chapter the main objects are described in detail.

### Job

The job object represents the whole build job the AM machine shall manufacture. It is the root object of the model. Contained in the job are two data objects: A list of WorkPlane objects and a map of MarkingParams objects. 
This data objects contain all information that is required for the machine to manufacture the job. Additionally, the job contains several metadata objects which are detailed in the next chapter. 
Most important of these metadata objects is the Part object map.

### WorkPlane

The WorkPlane object represents a two-dimensional drawing plane located in three-dimensional space, its name derives from the CAD concept with similar function. 
The work plane is probably the most defining object since it shows and limits the use case of the Open Vector Format. 
The object model aims at AM processes that use a motion system (e.g. (multi-)axis system, industrial robot) to position a build object 
(e.g. LPBF build plate, LMD part) relative to a vector based actuator (e.g. galvanometer scanner with laser source, magnetic field deflector with electron beam). The movements of both actuators are expected to happen 
consecutively and not simultaneous. Thus e.g. for LPBF the z-axis first moves the build plate into the correct height and after the movement is finished the laser actuator starts vector execution. 
Goal coordinates for the motion system are stored in the work plane object itself.

### VectorBlock

The VectorBlock object represents a set of vectors that share the same metadata and process parameter set. Each vector block is mapped to one specific set of marking parameters from the job via an index. 
The VectorBlock object exists mainly for performance reasons and storage space efficiency. Vector blocks can adapt one of several available types that define how exactly the point coordinate data is 
stored and shall be interpreted by the machine controller software. he most common VectorBlock types are “Hatches” and “LineSequences” (also known as polygones) that can also be found in CLI.
Hatches are defined as a set of straight lines that are not connected to each other and are commonly used to create the “filling” of parts. LineSequences are a set of connected straight line segments 
that are commonly used to create contours of AM parts. Vector block types act as a flexible extension point of the format. The machine controller software can check the vector block type and can only execute known types. 
If a specialized vector block type is beneficial for a use case, both the vector generating code as well as the machine controller can be extended to support other types while still 
utilizing the other parts of the job structure. For example arcs and ellipses have been added as additional vector block types. This geometric shapes can directly be executed by some 
galvanometer controller cards and are more efficient for manufacturing e.g. lattice structures than representing the circular contours with polygons. Additionally for multi-laser machines 
each vector block can store an index of the executing laser unit if the vector allocation is generated upfront and not on the machine.

### Marking Params

The MarkingParams object contains process parameters for the execution of the vectors like marking speed, power and abstract parameters for configuring the closed loop controller that 
controls the laser beams positional accuracy. This includes feed-forward parameters like delays as well as acceleration and deceleration compensation (“Skywriting”) set points like prerun 
and postrun times. It is up to the machine controller software to calculate the real set points from the abstract description considering the hardware components specifications, safety limits etc.

### Meta data
The basic objects Job, WorkPlane and VectorBlock contain additional fields for meta data related that object. The most relevant Metadata object is the Part. 
Many AM processes like LPBF create a whole batch of parts at once that get separated later. The information about the part relationship is not relevant for the printing process itself, but highly 
relevant for applications that process the data after slicing. Especially quality assurance applications need this relationship to connect data that is generated during or after AM processing like 
process monitoring sensor data and quality control measurements with the machine code.