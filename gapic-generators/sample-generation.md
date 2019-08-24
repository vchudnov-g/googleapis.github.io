# Auto-generating GAPIC samples

To generate GAPIC samples for your client library, you will need to configure
them in one or more YAML files. You can then request the generator produce
samples for your API by passing
`LANG_gapic_opt='samples=FILE1,samples=FILE2,samples=DIR'` to `protoc` when
you generate samples.

## Configuring your samples

You configure your samples via "sample-config" YAML docs. 
* Each doc can specify any number of samples for any RPC service and API for
which you are generating a GAPIC library.
* Any number of such sample-config docs can live in a single ``*.yaml`` file,
separated by the standard YAML document separator ``---``.
* You can provide any number of such files to a GAPIC generator. Any documents
(in any of the files) that don't self-identify as sample configs will be
silently ignored.

Each sample-config doc has the following structure:

```yaml
---
type: com.google.api.codegen.SampleConfigProto
schema_version: 1.2.0
samples:
- service: google.example.library.v1.MyProto
  rpc: PublishSeries
  description: An example showing how to list shelf contents
  request:
  …
  response:
  …
```

In the first two lines, the `type` and `schema_version` fields declare that this
is a sample config. The sample generators will ignore any YAML docs that do not
begin with these lines.

In the `samples` key, you provide a list of specifications for each sample that
you want to generate. Each specification contains two required fields (`service`
and `rpc`) to identify the RPC for which the method is being generated. Here you
can also specify additional metadata such as `title` and `description`.

The nitty-gritty of the sample configuration happens in the `request` and
`response` fields, which declare how to make API requests for this sample and
how to handle the resulting response.

### Constructing the request

The value of the `request` field is a list of items, each one corresponding to a
particular field or subfield of the RPC's request object to be set. Here's an
example:

```yaml
  request:
  - field: shelf.name
    comment: The name of the shelf where books are published to.
    value: Math
    input_parameter: shelf_name
  - field: edition
    comment: The edition of the series.
    value: '123'
    input_parameter: edition
    value_is_file: true
```

The items you can set in each element of the `request` list are as follows:
- `field` (required): A dotted notation path to a subfield of the request object for the RPC specified for this sample
- `input_parameter` (optional; defaults to `false`): Whether the value of this
  field will be hard-coded in the sample or can be specified as a CLI argument
  when running the sample
- `value` (required): The hard-coded value of this `field` (if `input_parameter`
  is false) or the default value of the corresponding CLI argument
- `comment` (optional): A comment that will appear in the sample describing this field
- `value_is_file` (optional, default to `false`): If true, the `value` of this
  field is treated as the name of a local file that will be opened and whose
  _contents_ will be assigned to `field`. This is useful, for example, if you
  want to pass image or audio data to your RPC.
  
  
### Handling the response

TODO: Fill in

### Full example

TODO: Fill in

## Generating the configured samples

TODO: Fill in how to generate

TODO: Link to next page on how to test



