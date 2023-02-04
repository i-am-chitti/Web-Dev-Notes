---
title: Chakra UI
created: '2022-04-19T10:22:12.071Z'
modified: '2022-04-19T16:34:01.043Z'
---

# Chakra UI

## Component

### Box
Box is the most abstract component on top of which all other Chakra UI components are built. By default, it renders a `div` element.

The Box component is useful because it helps with 3 common use cases:

- Create responsive layouts with ease.
- Provide a shorthand way to pass styles via props (bg instead of backgroundColor).
- Compose new component and allow for override using the as prop.

**Import**

```import { Box } from '@chakra-ui/react'```

**Usage**

```
<Box bg='tomato' w='100%' p={4} color='white'>
  This is the Box
</Box>
```

### Stack

Stack is a layout component that makes it easy to stack elements together and apply a space between them.

**Import**

```
import { Stack, HStack, VStack } from '@chakra-ui/react'
```

#### Vstack

The VStack component is a component which is only facing the vertical direction. Additionally you can add a divider and vertical spacing between the items.

#### Hstack

The HStack component is a component which is only facing the horizontal direction. Additionally you can add a divider and horizontal spacing between the items.

**Usage**

```
<HStack spacing='24px'>
  <Box w='40px' h='40px' bg='yellow.200'>
    1
  </Box>
  <Box w='40px' h='40px' bg='tomato'>
    2
  </Box>
  <Box w='40px' h='40px' bg='pink.100'>
    3
  </Box>
</HStack>
```

### Drawer

The Drawer component is a panel that slides out from the edge of the screen. It can be useful when you need users to complete a task or view some details without leaving the current page.

**Import**
```
import {
  Drawer,
  DrawerBody,
  DrawerFooter,
  DrawerHeader,
  DrawerOverlay,
  DrawerContent,
  DrawerCloseButton,
} from '@chakra-ui/react'
```

**Usage**

```
function DrawerExample() {
  const { isOpen, onOpen, onClose } = useDisclosure()
  const btnRef = React.useRef()

  return (
    <>
      <Button ref={btnRef} colorScheme='teal' onClick={onOpen}>
        Open
      </Button>
      <Drawer
        isOpen={isOpen}
        placement='right'
        onClose={onClose}
        finalFocusRef={btnRef}
      >
        <DrawerOverlay />
        <DrawerContent>
          <DrawerCloseButton />
          <DrawerHeader>Create your account</DrawerHeader>

          <DrawerBody>
            <Input placeholder='Type here...' />
          </DrawerBody>

          <DrawerFooter>
            <Button variant='outline' mr={3} onClick={onClose}>
              Cancel
            </Button>
            <Button colorScheme='blue'>Save</Button>
          </DrawerFooter>
        </DrawerContent>
      </Drawer>
    </>
  )
}
```

### Flex
Flex is Box with display: flex and comes with helpful style shorthand. It renders a div element.

**Import**
```import { Flex, Spacer } from '@chakra-ui/react'```

**Usage**
```
<Flex color='white'>
  <Center w='100px' bg='green.500'>
    <Text>Box 1</Text>
  </Center>
  <Square bg='blue.500' size='150px'>
    <Text>Box 2</Text>
  </Square>
  <Box flex='1' bg='tomato'>
    <Text>Box 3</Text>
  </Box>
</Flex>
```

#### Spacer
It creates equal spacing between the boxes in a flex box. If there are only two items, it will keep one at start and other at end.

```
<Flex>
  <Box p='4' bg='red.400'>
    Box 1
  </Box>
  <Spacer />
  <Box p='4' bg='green.400'>
    Box 2
  </Box>
</Flex>
```

#### Navbar with this

```
<Flex>
  <Box p='2'>
    <Heading size='md'>Chakra App</Heading>
  </Box>
  <Spacer />
  <Box>
    <Button colorScheme='teal' mr='4'>
      Sign Up
    </Button>
    <Button colorScheme='teal'>Log in</Button>
  </Box>
</Flex>
```

#### Flex and spacer vs grid vs stack

```
<Box>
  <Text>Flex and Spacer: Full width, equal Spacing</Text>
  <Flex>
    <Box w='70px' h='10' bg='red.500' />
    <Spacer />
    <Box w='170px' h='10' bg='red.500' />
    <Spacer />
    <Box w='180px' h='10' bg='red.500' />
  </Flex>

  <Text>
    Grid: The children start at the beginning, the 1/3 mark and 2/3 mark
  </Text>
  <Grid templateColumns='repeat(3, 1fr)' gap={6}>
    <Box w='70px' h='10' bg='blue.500' />
    <Box w='170px' h='10' bg='blue.500' />
    <Box w='180px' h='10' bg='blue.500' />
  </Grid>

  <Text>
    HStack: The children have equal spacing but don't span the whole container
  </Text>
  <HStack spacing='24px'>
    <Box w='70px' h='10' bg='teal.500' />
    <Box w='170px' h='10' bg='teal.500' />
    <Box w='180px' h='10' bg='teal.500' />
  </HStack>
</Box>
```

## Hooks

### useDisclosure

useDisclosure is a custom hook used to help handle common open, close, or toggle scenarios. It can be used to control feedback component such as Modal, AlertDialog, Drawer, etc.

**Import**

```import { useDisclosure } from '@chakra-ui/react'```

**Example**

```
function Example() {
  const { isOpen, onOpen, onClose } = useDisclosure()

  return (
    <>
      <Button onClick={onOpen}>Open Drawer</Button>
      <Drawer placement='right' onClose={onClose} isOpen={isOpen}>
        <DrawerOverlay />
        <DrawerContent>
          <DrawerHeader borderBottomWidth='1px'>Basic Drawer</DrawerHeader>
          <DrawerBody>
            <p>Some contents...</p>
            <p>Some contents...</p>
            <p>Some contents...</p>
          </DrawerBody>
        </DrawerContent>
      </Drawer>
    </>
  )
}
```

### useColorMode

useColorMode is a React hook that gives you access to the current color mode, and a function to toggle the color mode.

```
function Example() {
  const { colorMode, toggleColorMode } = useColorMode()
  return (
    <header>
      <Button onClick={toggleColorMode}>
        Toggle {colorMode === 'light' ? 'Dark' : 'Light'}
      </Button>
    </header>
  )
}
```

### useColorModeValue

useColorModeValue is a React hook used to change any value or style based on the color mode. It takes 2 arguments: the value in light mode, and the value in dark mode.

```
// Here's the signature
const value = useColorModeValue(lightModeValue, darkModeValue)
```

```
function StyleColorMode() {
  const { toggleColorMode } = useColorMode()

  const bg = useColorModeValue('red.500', 'red.200')
  const color = useColorModeValue('white', 'gray.800')

  return (
    <>
      <Box mb={4} bg={bg} color={color}>
        This box's style will change based on the color mode.
      </Box>
      <Button size='sm' onClick={toggleColorMode}>
        Toggle Mode
      </Button>
    </>
  )
}
```

## Responsive Styling

Chakra UI allows you to provide object and array values to add mobile-first responsive styles. It uses the @media(min-width) media query to ensure your interfaces are mobile-first.

Responsive syntax relies on the breakpoints defined in the theme object. Chakra UI provides default breakpoints, here's what it looks like:

```
const breakpoints = {
  sm: '30em',
  md: '48em',
  lg: '62em',
  xl: '80em',
  '2xl': '96em',
}
```

### Array syntax

All style props accept arrays as values for mobile-first responsive styles. This is the recommended method.

```
<Box bg='red.200' w={[300, 400, 500]}>
  This is a box
</Box>

// These are the default breakpoints
const breakpoints = {
  sm: '30em',
  md: '48em',
  lg: '62em',
  xl: '80em',
  '2xl': '96em',
}

// Internally, we transform to this
const breakpoints = ['0em', '30em', '48em', '62em', '80em', '96em']
```
To interpret array responsive values, Chakra UI converts the values defined in `theme.breakpoints` and sorts them in ascending order. Afterward, we map the values defined in the array to the breakpoints

Here's how to interpret this syntax:

- 300px: From 0em upwards (0-29em)
- 400px: From 30em upwards (30em-47em)
- 500px: From 48em upwards (48em+)

### Object syntax

You can also define responsive values with breakpoint aliases in an object. Any undefined alias key will define the base, non-responsive value.

```
<Text fontSize={{ base: '24px', md: '40px', lg: '56px' }}>
  This is responsive text
</Text>
```
Here's how to interpret this syntax:

- base: From 0em upwards (0-47em)
- md: From 48em upwards (48em-61em)
- lg: From 62em upwards (62em+)

**NOTE** - If you're using pixels as breakpoint values make sure to always provide a value for the 2xl breakpoint, which by its default pixels value is "1536px".

## Global Styles

GlobalStyle is a new component in v1 that injects styles defined in theme.styles.global into the global styles of your app or website.

This allows you define theme-aware styles for any elements.

```
// 1. Using a style object
const theme = {
  styles: {
    global: {
      'html, body': {
        color: 'gray.600',
        lineHeight: 'tall',
      },
      a: {
        color: 'teal.500',
      },
    },
  },
}

// 2. Using a function
// NB: Chakra gives you access to `colorMode` and `theme` in `props`
const theme = {
  styles: {
    global: (props) => ({
      'html, body': {
        fontSize: 'sm',
        color: props.colorMode === 'dark' ? 'white' : 'gray.600',
        lineHeight: 'tall',
      },
      a: {
        color: props.colorMode === 'dark' ? 'teal.300' : 'teal.500',
      },
    }),
  },
}
```
### Default styles
```
import { mode } from '@chakra-ui/theme-tools'

const styles = {
  global: (props) => ({
    body: {
      fontFamily: 'body',
      color: mode('gray.800', 'whiteAlpha.900')(props),
      bg: mode('white', 'gray.800')(props),
      lineHeight: 'base',
    },
    '*::placeholder': {
      color: mode('gray.400', 'whiteAlpha.400')(props),
    },
    '*, *::before, &::after': {
      borderColor: mode('gray.200', 'whiteAlpha.300')(props),
      wordWrap: 'break-word',
    },
  }),
}
```

**Note** - `mode(lightMode, darkMode)(props)` function is the same as `props.colorMode === "dark" ? darkMode : lightMode`











