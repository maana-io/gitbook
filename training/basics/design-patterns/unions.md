# Unions

## Problem

Along with specialization, we often need to have a collection of a concept or any of its specializations

e.g., if we simply had a collection of Parts, we would not be able to distinguish RotatingPart from ElectricalPart

The solution is to create a new type called a union which contains relations for each of the allowed specializations, for which there will only ever be one

e.g., PartUnion { electricalPart: ElectricalPart, rotatingPart: RotatingPart, hydraulicPart: HydraulicPart, rotatingElectricalPart: RotatingElectricalPart }

A union can now be used as a relation or in a function as any other Kind

e.g., WorkOrder { part: PartUnion, ... }

## Solution

